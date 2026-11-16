# Issue

**Title:** Allow submatrix extraction to skip coercion to an ordinary matrix.

## Description

This is useful to avoid unnecessary loss of sparsity, e.g., if the submatrix is to be used in more calculations before the actual plotting.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2d0c7818497a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.