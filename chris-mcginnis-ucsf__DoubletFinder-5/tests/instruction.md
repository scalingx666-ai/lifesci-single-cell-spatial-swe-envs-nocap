# Issue

**Title:** Fixed out of bounds error and changed cells used for doublet calculation

## Description

Added the PCs variable to the RunPCA function so that when RunPCA is executed, it will calculate the same number of PCs that was used to calculate the original Seurat object.

This will resolve #3 and #6.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6fb716b2ef9e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.