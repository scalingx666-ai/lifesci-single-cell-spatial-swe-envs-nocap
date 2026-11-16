# Issue

**Title:** Ensure PCA initialization has small variance

## Description

- As per #10, it is vital for tSNE optimization that the initialization has small variance. Without this scaling, PCA initialization can potentially lead to really bad results.

- Remove `pca` option when embedding new points into an existing embedding. This makes no sense because likely the points in the original space would have moved significantly and adding new points would be meaningless.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `32f9b04a9a52`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.