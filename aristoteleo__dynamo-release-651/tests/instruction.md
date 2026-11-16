# Issue

**Title:** Debug plot/preprocess.py

## Description

Bug description:

- `biplot()` and `loading()` both plot the PCA embedding. So they should use cells as text labels instead of genes.
- `feature_genes` should support all type of gene selection methods.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1eaafae718db`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.