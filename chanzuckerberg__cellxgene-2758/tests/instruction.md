# Issue

**Title:** fix: Handle non-categorical columns with colors + update deprecated AnnData API

## Description

### Problem

Cellxgene crashes when loading AnnData files with boolean (or other non-categorical) columns that have associated colors in `adata.uns`:

```
AttributeError: Can only use .cat accessor with a 'category' dtype. Did you mean: 'at'?
```

The color conversion code assumes all columns with colors are categorical and directly accesses `.cat.categories`, which fails for boolean dtypes (which are common for QC, like 'is_doublet' or similar).

### Solution

Updated color handling to convert non-categorical columns to categorical before accessing categories.

Also: replaced deprecated AnnData API calls with modern equivalents (supported since AnnData 0.7.0, deprecated in 0.12.3) to avoid warnings.

### Changes

**add:**
- Import `importlib.metadata` in `anndata_adaptor.py` to replace deprecated version checking

**remove:**
- Deprecated AnnData method calls: `.obsm_keys()`, `.obs_keys()`, `.var_keys()`, `.uns_keys()`, `.__version__`

**modify:**
- `server/data_common/colors.py`: Updated `convert_anndata_category_colors_to_cxg_category_colors()` to use `.astype('category')` for non-categorical columns before accessing categories
- `server/data_anndata/anndata_adaptor.py`: Replaced `.__version__` with `importlib.metadata.version('anndata')` and deprecated key methods with dictionary-style access
- `server/data_anndata/prepare.py`: Updated to use `.obs.keys()` and `.var.keys()` instead of deprecated methods
- `server/data_common/corpora.py`: Updated to use `.uns.keys()` instead of deprecated methods

### Testing

- Boolean column datasets now load without crashes
- Categorical column behavior unchanged
- All deprecation warnings eliminated

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7c7203bdfe52`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.