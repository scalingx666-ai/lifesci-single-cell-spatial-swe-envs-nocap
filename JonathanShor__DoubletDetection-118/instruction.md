# Issue

**Title:** Sparse raw counts and UMAP

## Description

-  
- Reduces memory overhead of storing both normed counts and raw counts as dense
- Reduces per iteration speed by about 3 seconds on laptop
- Exchanges TSNE with UMAP for visualization (much faster)
- If a dense `raw_counts` is entered into `.fit()` it will automatically be sparsified

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a34777cd03de`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.