# Issue

**Title:** Changed dependency versions

## Description

`anndata` 0.10.0 updated changed a class name from `SparseDataset` to `BaseCompressedSparseDataset` and `scvi-tools` has not updated to be compatible yet.
Changing `anndata` to 0.9.2

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d2dcd9eda736`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.