# Issue

**Title:** Resolve Windows parallelization issues and internal processing bugs for improved stability and performance

## Description

**Improvements and Fixes:**
1. Use `BiocParallel::SnowParam()` automatically when running on Windows for compatibility.
2. Significantly accelerate `SPLIT::run_post_process_RCTD()` by eliminating unnecessary expensive computations.
3. Optimized `SPLIT::purify()` to streamline chunk processing, making the non-parallel version nearly as efficient as the parallel one and setting it as the new default for improved simplicity and performance.
4. Fix bug in `SPLIT::purify()` when spot_class contains empty categories (addresses issue #7).

All changes are backward compatible.
Bump package version to **0.1.1.**

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cd90fa7572b7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.