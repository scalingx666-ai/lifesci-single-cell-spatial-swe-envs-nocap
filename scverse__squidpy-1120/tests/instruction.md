# Issue

**Title:** feat: remove unnecessary parallelize usage in sepal

## Description

hi, 

from the rsc sepal implementation I know we can get rid of `parallelize` easily. I also have a longer term plan to remove parallelize. I checked with this script: https://gist.github.com/selmanozleyen/c4b0e4780243fd4621f68bc2d78cae5c

Results pretified with AI:

### Benchmark results (502 genes, 2688 cells, visium_hne_adata, 3 runs, 8 cores)

| variant                                |   mean |  median |    min |    max |
|----------------------------------------|--------|---------|--------|--------|
| main, n_jobs=1 (sequential)            | 134.9s | 134.4s  | 134.3s | 136.0s |
| main, n_jobs=6 (joblib/loky)           |  40.5s |  40.2s  |  37.9s |  43.5s |
| this PR, prange (no pre-alloc)         |  37.7s |  37.6s  |  36.9s |  38.6s |
| this PR, prange + pre-alloc buffers    |  31.9s |  31.3s  |  30.9s |  33.6s |



## Motivation

This PR replaces the internal `parallelize` + `joblib.Parallel` machinery in
`sepal()` with Numba's native `prange` threading, removing the need for
multi-process orchestration (subprocess spawning, pickling, IPC).

### Key changes

1. **`prange` over genes** -- The outer gene loop is parallelized with
   `numba.prange` inside a `@njit(parallel=True)` function, replacing
   `joblib.Parallel(n_jobs=..., backend="loky")`.



2. **Pre-allocated per-thread workspace buffers** (this commit ) You can see why I did this in https://numba.readthedocs.io/en/stable/user/parallel.html#diagnostics under "allocation hoisting"

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3b3df066687c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.