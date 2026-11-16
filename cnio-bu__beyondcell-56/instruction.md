# Issue

**Title:** Add two new parameters to bcUMAP

## Description

- `npcs`: Total Number of PCs to compute and store.
- `seed`: Random seed for `RunPCA` and `RunUMAP`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e3ef5d18e6bd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.