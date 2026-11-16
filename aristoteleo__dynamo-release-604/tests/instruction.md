# Issue

**Title:** Debug highest_frac_genes

## Description

Bug description: When `gene_X_percents` is a sparse matrix, `np.array(gene_X_percents)` will raise an error.

Solution: Use `toarray()` instead of `np.array()` for sparse matrix.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1e8ffe4a103e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.