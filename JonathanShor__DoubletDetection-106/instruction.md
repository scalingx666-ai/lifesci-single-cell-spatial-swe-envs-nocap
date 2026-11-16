# Issue

**Title:** Random seed

## Description

- Adds `random_state` parameter which controls synthetic doublet creation, PCA, as well as PCA and TSNE in `.plot`
- Updates thresholds in PBMC8k notebook

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `33362e6b7b0e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.