# Issue

**Title:** fix(sparsify): materialize transport-matrix rows instead of pushing indicator columns

## Description

## Problem

`sparsify` extracts rows of the transport matrix by pushing dense identity blocks:

```python
rows = np.asarray(self.push(np.eye(n, cols, -batch), scale_by_marginals=False)).T
```

`ott`'s log-sum-exp apply materializes an `[n, m, k]` tensor for a `k`-column input, so peak memory is `n · m · batch_size`, not `batch_size` as the docstring promises. Measured on `main` (moscot 0.5.1, ott-jax 0.6.0 and `main`, jax 0.11.1), for a `TemporalProblem` whose dense couplings are 18 MB at n = m = 1500:

| `sparsify_kwargs={"batch_size": …}` | 8 | 64 | 256 | 1024 (default) |
|---|---|---|---|---|
| peak RSS | 0.7 GB | 1.7 GB | 5.8 GB | **17.8 GB** |

Isolated at the `ott` level, `output.apply` on an `[n, k]` input peaks at ≈ `3 · n · m · k · 4` bytes. At n = m = 8000 the default `batch_size` would need ~262 GB to sparsify a 256 MB plan. The knob you have to shrink to survive is also the one that makes the result worse (below), and #843's row-oriented loop did not change this — it fixed the orientation but kept the identity push.

This is what large-data users hit downstream: scverse/cellrank#1146.

## Fix

Rows are built directly, behind one seam — `BaseDiscreteSolverOutput._row_materializer()`, a factory returning a callable over row indices (built once per `sparsify` call, so per-output work such as resolving a geometry is hoisted out of the block loop):

- **low-rank** (`LRSinkhornOutput`, `LRGWOutput`): `T[rows] = (Q diag(1/g) Rᵀ)[rows]`, exactly `ott`'s own `matrix`. Never touches a geometry — which matters, since `LRGWOutput.geom` re-linearizes on every access.
- **entropic** (`SinkhornOutput`, and `GWOutput` via `linear_state`): `T[rows] = exp((f_i + g_j − C_ij) / ε)`, with the cost rows from `cost_fn.all_pairs(x[rows], y)` (`PointCloud`), `cost_1[rows] @ cost_2ᵀ + bias` (`LRCGeometry`) or `cost_matrix[rows]` (dense `Geometry`).
- **`MatrixSolverOutput`**: slices what it already holds.
- **anything else** — notably `GraphOTTOutput`, whose geometry is a `Geodesic` and whose rows are a sub-block of an expanded `(n+m)²` problem — keeps the push-based default, which is cheap there: applying a sparse graph kernel costs `nnz` per column, not `n · m`.

Two correctness traps this had to avoid, both verified:

- **`geom.subset(row_ixs=…)` cannot be used.** `scale_cost` and `relative_epsilon` travel as unevaluated strings in `aux_data`, so a subset geometry re-derives `inv_scale_cost` and `epsilon` from the subset. With `scale_cost="mean"` (what `moscot` solves with) that shifted `inv_scale_cost` 0.05235 → 0.05396 and produced **15% value error**, silently. The materializer captures the parent's resolved values instead. `LRCGeometry.subset` is worse — the inherited `Geometry.subset` slices the two factors as if they were cost/kernel.
- **`GWOutput._rescale_factor`** (`sqrt(old_transport_mass / linear_state.transport_mass)`) must be applied, as `matrix` and `apply` both do. It is ~1.0 on converged balanced problems, so it hides easily; there is a test that forces it to 2.0.

### Results

Peak memory at n = m = 1500 drops from **17.8 GB to 84 MB** (212×) and no longer scales with `batch_size` (ratio across 64 → 1024 goes from 4.8× to 0.6×); `min_row` is now cheaper than materializing the dense plan. Reconstruction is bit-exact (`rel_err = 0.0`) for Sinkhorn (offline / online / low-rank-cost geometry), low-rank Sinkhorn, GW, low-rank GW and FGW, across `scale_cost ∈ {1.0, "mean", "max_cost"}`.

## Behavioural changes

**`min_row` is now exact and independent of `batch_size`.** The intent — the largest threshold that keeps every row, `min_i max_j T_ij`, so the result can still be normalized into a Markov chain — was computed over *column* batches, which can only underestimate it. At n = m = 1500 it kept 182,645 entries at `batch_size=1024` and 1,227,714 at 64, against **2,319** for the exact rule; the threshold and the values also came from two different float paths (`pull` vs `push`), which could empty a row outright (I measured 199/200 rows non-empty at `batch_size = m`). Results are **unchanged whenever `m <= batch_size`**, which is why small problems never showed this; users with `m > batch_size` will see much sparser couplings.

**Rows carrying no mass are handled centrally**, for every mode: they keep no entries and take no part in choosing a threshold. No threshold can make them non-empty, while letting them participate drags any row-based threshold to 0 and disables sparsification altogether (a single massless row took a test matrix from 21% to 88% dense). A warning is emitted, since the result then cannot be normalized into a Markov chain. `mass` mode already behaved this way; the modes are now consistent.

**`percentile`** estimates its threshold from sampled rows rather than pulled column indicators, so it uses the same bounded path as everything else.

**`OTTOutput._with_batch_size` is removed.** It only ever rebatched a Sinkhorn output over an online `PointCloud` — exactly the case now built from potentials — so it became dead code.

## Tests

- `tests/solvers/test_base_solver.py`: `min_row` independence from `batch_size`, the every-row-non-empty contract, exactness against `min_i max_j T_ij`, `percentile` row sampling, metadata propagation, a `TestMinRowStructure` class checking the `pull` proxy on a transport-plan-like matrix, and a `TestMasslessRows` class covering all four modes.
- `tests/backends/ott/test_backend.py`: `TestSparsifyRows` — reconstruction across 7 output flavours × 3 `scale_cost` × 3 `batch_size`, a monkeypatched `push`/`pull`/`transport_matrix` that must never be called, the `min_row` contract on real outputs, a parent-`scale_cost` check, and the forced GW rescale factor.
- `tests/backends/ott/test_sparsify_memory.py`: strict peak-RSS tests, each in a fresh subprocess (peak RSS is process-global and `xdist` would confound it). Marked `memory` and **deselected by default** (`addopts = -m 'not memory'`), since they are environment-sensitive and deliberately large enough that the old implementation exhausts memory; run them with `pytest -m memory`.

The new tests are discriminating: **37 fail against the current `main` sources** and all pass with the fix.

One pre-existing test changed: `test_sparsify_minrow`'s `corrcoef(pull_sparse, pull_dense) > 0.5` proxy encoded the old, denser output — on a *uniform random* fixture the exact rule keeps ~1 entry per row, which cannot correlate with the dense pull. It is replaced by an exactness assertion, and the proxy is retained in `TestMinRowStructure` on a peaked, plan-like matrix where it is meaningful.

## Verification

Full suite: 839 passed. The 27 failures in `test_annotation_mapping` / `test_set_graph_xy` are pre-existing in my environment (ott-jax `main` + jax 0.11) — identical counts with and without this change. `black`/`isort`/`ruff` clean. End-to-end from cellrank (`RealTimeKernel.from_moscot(..., sparse_mode="min_row")`, n = m = 1500): sparse couplings, no empty rows, row-stochastic transition matrix, and its `test_from_moscot` tests pass.

Out of scope, filed separately: `GraphOTTOutput` overrides `shape` but inherits `transport_matrix` from `OTTOutput`, returning the full expanded `(n+m)²` matrix.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1d4a4bcd6f51`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.