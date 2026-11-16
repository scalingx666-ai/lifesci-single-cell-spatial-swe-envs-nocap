# Issue

**Title:** Fix missing imports

## Description

Liger seems to have been using `base::rowSums` and `base::colSums`, which don't work on sparse matrices. This PR imports `rowSums` and `colSums` from Matrix, which support both dense and sparse matrices, and exposes it to the majority of Liger's codebase.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2623af2b9140`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.