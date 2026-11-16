# Issue

**Title:** Fix compatibility with anndata >= 0.12

## Description

TISSUE 1.0.1 breaks with recent anndata and has several smaller issue in `tissue/main.py`:

I patched the [fixes in bioconda](https://github.com/bioconda/bioconda-recipes/tree/master/recipes/tissue-sc) and here is the same fix proposed.
These changes are tested with the galaxy tool.

It will close this issue

- `AnnData.__init__(dtype='float32')` is used at three call sites.
   The `dtype` kwarg was removed from anndata;
  dropped the kwarg and cast `X` with `.astype('float32')` instead.
- `build_spatial_graph` ignores its `spatial` parameter: the
  `spatial_key=` argument is never forwarded to
  `sq.gr.spatial_neighbors` (call sites around lines 190-237).
  Coordinates are therefore always read from `adata.obsm['spatial']`
  regardless of the parameter.
- When `radius=None` is selected, the value is stored verbatim in
  `adata.uns['spatial_neighbors']['params']`. anndata >= 0.12.1
  serializes `None` with a `null` encoding that older readers cannot
  parse, breaking h5ad round-trips. `None` is now omitted from
  `params`.
- `predict_gene_expression` lowercases and deduplicates `var_names`
  of the input AnnData objects in place, mutating the caller's data.
  The transformation is now applied on a copy.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ffc35998004e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.