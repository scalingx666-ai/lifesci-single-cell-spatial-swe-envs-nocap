# Issue

**Title:** Add normalize_shifted_clr matching scanpy

## Description

Adds `rsc.pp.normalize_shifted_clr`, a GPU port of scanpy's `sc.pp.normalize_shifted_clr` (scverse/scanpy#4160): PFlog, the shifted centered log-ratio of Booeshaghi et al.

```
T(x)_i = log1p(4·α·x_i) − mean_j log1p(4·α·x_j)
```

`α` is the negative-binomial overdispersion. If it is not given, it is estimated by closed-form least squares of `var = μ + α·μ²` across genes.

This replaces the earlier `normalize_clr` draft. That draft depth-normalized every cell to a target `K` before `log1p`, took `target_sum`, and wrote a factored `layers["clr"]` + `obsm` output, so its results differed from what scanpy merged. The factored PCA follow-up (#703) is closed.

**Matches scanpy**
- Same signature (`alpha`, `layer`, `inplace`, `copy`), defaults, errors and the "Some cells have zero counts" warning.
- The output is dense, as in scanpy, written to `X` or the layer; `inplace=False` returns `{"X": ...}`.
- Integer input is converted to float64 and CSC to CSR, as in scanpy.

**GPU**
- Two new `_norm_cuda` kernels, `shifted_clr_csr` and `shifted_clr_dense`, run one block per row: the block sums `log1p(4αx)` in float64, then writes the centered dense row directly. The CSR kernel fills the row with the negated mean, then scatters the stored values.
- Dense and Dask input (row chunks, CSR or dense) are supported.
- `_get_mean_var` gets a `correction` keyword so `α` uses the population variance (`correction=0`).
- On 1M cells × 200 features (CSR, float32, GB10): 50 ms with `α` given and 94 ms with `α` estimated, vs 1.15 s for scanpy on the CPU.

**Tests**
- `tests/test_shifted_clr.py` ports scanpy's tests to CuPy dense, CSR and CSC.
- They also compare live against scanpy's own `normalize_shifted_clr` and its α estimate: within 1e-12 for float64 and 1e-6 for float32. Released scanpy doesn't have the function yet, so these tests skip there and run in the `dev` CI env (scanpy main); a TODO marks the skip for removal once scanpy releases it.
- New Dask tests, plus `correction` cases for the mean/var tests.

The first two commits are the old draft rebased onto main; the last one replaces it, so please squash-merge.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8d8eb2b36c37`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.