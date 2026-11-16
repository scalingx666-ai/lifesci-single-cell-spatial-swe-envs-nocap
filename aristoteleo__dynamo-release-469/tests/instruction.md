# Issue

**Title:** Optimize pca

## Description

Main optimization:

- Implement _truncatedSVD_with_center to perform PCA directly on sparse matrix
- Enable Incremental PCA to control the memory usage
- Change the PCA method to Randomized PCA for better efficiency. Make random state as an argument to ensure the reproducibility

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ba43701ca1ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.