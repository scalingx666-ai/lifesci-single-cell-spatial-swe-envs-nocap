# Issue

**Title:** Input formats

## Description

- Accept "array-like", which includes DataFrames

- Made the decision to throw an error if a sparse matrix is input because our code makes no optimization for this 

- Load mtx function for cell ranger outputs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b7bc63898aa5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.