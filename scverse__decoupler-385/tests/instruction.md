# Issue

**Title:** Fix mt.waggr crash under numba workqueue threading layer

## Description

## Problem

`mt.waggr` with permutations (`times > 1`) aborts the whole Python process (`Fatal Python error: Aborted`) when numba falls back to the `workqueue` threading layer, which is the default when TBB and OpenMP are unavailable (e.g. pip installs on macOS arm64):

```
Numba workqueue threading layer is terminating: Concurrent access has been detected.
```

`_perm` is `parallel=True` and, inside its `prange(times)` loop, calls the per-function kernel built in `_fun`, which is also `parallel=True`. This nested parallel region works with `omp`/`tbb` but is not supported by `workqueue`. `times=0` was unaffected.

## Fix

`_fun` now compiles two kernels: the parallel one is still used for the observed scores, and a serial one is passed to `_perm`, so the only parallelism is the outer permutation loop.

## Tests

Added `test_waggr_workqueue`, which runs waggr in a subprocess with `NUMBA_THREADING_LAYER=workqueue` (a subprocess is needed since the failure kills the interpreter). It fails on `main` and passes with this change.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7a6e70de19e6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.