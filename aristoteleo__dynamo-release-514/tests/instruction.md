# Issue

**Title:** Add X_PCA as special key in DKM and remove .obsm.["X"]

## Description

remove adata.obsm[X] in future, use adata.obsm.X_pca instead.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a9b39580733c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.