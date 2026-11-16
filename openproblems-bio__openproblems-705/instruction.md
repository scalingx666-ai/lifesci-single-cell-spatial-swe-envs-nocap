# Issue

**Title:** Add spectral baseline to dimensionality reduction

## Description

The high-dimensional PCA does well in global metrics, but poorly in local knn metrics. This baseline (200-dimensional laplacian eigenmaps) should perform well with local knn ranking metrics.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f42dcb4e4c16`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.