# Issue

**Title:** Memory-bounded sparsify + per-row mass mode

## Description

## Summary

Fixes the out-of-memory failure when materializing a sparse transport matrix from an online (linear Sinkhorn) `PointCloud` solution — the case behind scverse/cellrank#1146 — and adds a predictable per-row sparsification mode.

One sparsify *algorithm* in the base class, identical for every output type; OTT contributes only a geometry-reconfiguration step. .

## What & why

`BaseDiscreteSolverOutput.sparsify` materializes the transport matrix in row blocks via `push`/`pull`. For an **online `PointCloud`** geometry the cost is recomputed lazily during `apply`, chunked by `geom.batch_size` — which is **frozen at `solve()` time** and cannot be lowered from `sparsify`. A large solve-time batch therefore OOMs during sparsify, even on CPU (#639).

### 1. `batch_size` now bounds peak memory (`OTTOutput.sparsify`)

`OTTOutput.sparsify` rebuilds the online geometry with the requested `batch_size` (via the geometry pytree, preserving `scale_cost`/`relative_epsilon`/`epsilon`/`cost_fn`/`x`/`y`), then delegates to the base algorithm. It is a **no-op** for anything that is not an online `PointCloud` Sinkhorn output — the same algorithm, the knob is simply inert where there is no lazy cost to retune.

### 2. New `mode="mass"`

Per source row, keep the largest entries capturing a fraction `value` of the row's mass, capped at `max_k` — bounded, predictable nnz. The block loop is unified on the source axis so each block holds rows of `T`; element-wise modes (`threshold`/`percentile`/`min_row`) are unchanged and transpose-invariant.

### What this does per problem type

| Problem | Rank | Coupling stored as | online `batch_size`? | rebatch | effect |
|---|---|---|---|---|---|
| Linear | full | `f,g` on lazy/online `PointCloud` | yes | **lowers it** | **only case changed — bounds the OOM** |
| Linear | low | factors `Q,R,g` | no | no-op | already bounded |
| GW | full | dense `[n,m]` linearized cost | no | no-op | dense by construction |
| GW | low | factors (`LRGWOutput`) | no | no-op | already bounded |
| FGW | full | as GW-full (+ fused term) | no | no-op | dense |
| FGW | low | factors | no | no-op | already bounded |

## Tests

- **Base** (`tests/solvers/test_base_solver.py`): exact-reconstruction oracle (`value=1.0, max_k=None` reproduces the transport matrix), mass retention, `max_k` cap, validation — on dense `MockSolverOutput` for both `n<m` and `n>m`.
- **OTT backend** (`tests/backends/ott/test_backend.py`): online rebatch reconstruction across `scale_cost ∈ {1.0, 0.5, mean, max_cost, max_norm, max_bound}` × balanced/unbalanced; rebatch mechanics; no-op guards for offline / `median` / low-rank / GW.

> [!NOTE]
> The online-`PointCloud` backend tests are skip-guarded: ott-jax ≤ 0.6.0 (and currently `main`) rely on `jax.interpreters.batching.is_vmappable`, removed in jax ≥ 0.9, which breaks any online apply (). They are validated to pass where the online path works and skip otherwise; the base-class tests cover the core logic regardless.

## Links

-
- Surfaces for users in scverse/cellrank#1146
- ott-jax/jax compatibility tracked in #842

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bacec6c7a4bf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.