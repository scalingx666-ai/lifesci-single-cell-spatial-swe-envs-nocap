# Issue

**Title:** Fix Numba workqueue abort in feature streams

## Description

## Summary
- prevent concurrent entry into Numba workqueue parallel regions
- run always-pooled kernels as serial GIL-free computations
- serialize marker adapters that retain Numba inner parallelism
- add a forced-workqueue subprocess regression

## Impact
Public signatures and persisted artifacts are unchanged. RNA feature summaries and rank marker searches complete safely with multiple Scarf workers under the workqueue backend.

## Performance concern
Default matrix layouts can yield only one outer stream task. In that case, the newly serial kernels cannot use the full worker budget. This should be resolved before merge if preserving OpenMP performance is required.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `380fe4ac1c24`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.