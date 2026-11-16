# Issue

**Title:** conditional loading of DelayedMatrixStats

## Description

`RowSums2` requires `DelayedMatrixStats` if the count matrix is of class `dgCMatrix`. Added `DelayedMatrixStats` to suggested packages in `DESCRIPTION` and implemented conditional loading of the package if the count matrix is sparse.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c260ec6378ef`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.