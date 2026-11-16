# Issue

**Title:** Spatial KNN-cu12 neighbors compilation fix

## Description

Every extension is a single translation unit without cross-file device calls, so relocatable device code buys nothing. Together with nanobind's LTO option it turns on device LTO, and the cu12 wheels built that way (CUDA 12.2) return non-finite spatial kNN distances from the register top-k kernels (kd_search<T, 8/16/32>, k <= 32) on every GPU, including when their Hopper code is JIT-compiled on Blackwell. The same source compiled whole-program is correct. Compile each module whole-program.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `243f4737f7c1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.