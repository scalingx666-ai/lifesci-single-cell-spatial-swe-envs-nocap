# Issue

**Title:** add warning for degenerate diffusion operator

## Description

Added graceful error handling for degenerate distance matrices in PHATE's MDS embedding step. When KNN is close to dataset size, diffusion homogeneity causes all-zero distance matrices. Instead of crashing with Procrustes error, now returns zero embedding with RuntimeWarning explaining the hyperparameter issue.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ec7d6ea28909`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.