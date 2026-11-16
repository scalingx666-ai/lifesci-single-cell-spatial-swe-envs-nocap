# Issue

**Title:** fix: don't warn from log1p about X when transforming a layer or obsm

## Description

`sc.pp.log1p` warns "adata.X seems to be already log-transformed" whenever `adata.uns["log1p"]` exists, even when the call targets a layer or obsm and never touches `X`:

```python
sc.pp.log1p(adata)
sc.pp.log1p(adata, layer="spliced")    # WARNING: adata.X seems to be already log-transformed.
sc.pp.log1p(adata, layer="unspliced")  # WARNING: adata.X seems to be already log-transformed.
```

The `uns` marker only ever describes `X`, so this PR just skips the warning when `layer` or `obsm` is given. No change to what is stored in `uns`, so nothing downstream (`highly_variable_genes`, `rank_genes_groups`) is affected.

Added a small test for the three cases (`X` warns, `layer`/`obsm` don't); it fails on `main` and passes here. `pytest tests/test_preprocessing.py tests/test_highly_variable_genes.py tests/test_rank_genes_groups.py`: 590 passed. Ruff clean.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `82db34ee653f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.