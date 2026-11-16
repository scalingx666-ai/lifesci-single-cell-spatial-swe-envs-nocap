# Issue

**Title:** fix(latentvelo): restore preprocessing compatibility

## Description

## Summary

Restore LatentVelo preprocessing compatibility with current scVelo and AnnData releases.

- Replace the removed `scvelo.preprocessing.filter_genes_dispersion` calls with OmicVerse-native HVG selection.
- Preserve the former HVG-selection semantics by running the `seurat` selector on a temporary log1p-transformed expression matrix.
- Keep the original recipe `X` and layers unchanged during HVG selection, while avoiding a deep copy of the complete AnnData object.
- Preserve CSR output after row-wise library-size normalization so AnnData 0.12+ accepts updated layers.
- Restore `n_top_genes` subsetting in the ATAC recipe.


The removed scVelo selector and OmicVerse’s `seurat` HVG implementation expect equivalent log1p expression semantics for ranking highly variable genes. LatentVelo performs its own log transform later in the recipe, so passing its library-normalized counts directly to `ov.pp.highly_variable_genes` would change the selected genes.

`_select_hvgs_from_log1p` creates a lightweight temporary AnnData containing only a copied `X` matrix and `var` metadata, applies log1p only to that temporary matrix, and transfers the HVG annotations back. This preserves the previous selection behavior without mutating the layers used by downstream velocity preprocessing or duplicating large layers and graphs.

## Validation

- Reproduced the removed scVelo API failure with scVelo 0.3.4.
- Verified CSR-preserving row normalization for sparse layers.
- Ran the LatentVelo standard-recipe compatibility smoke test through HVG selection, PCA, neighbor construction, and moments.
- Verified the temporary HVG selection leaves the original `X` unchanged and restores ATAC gene subsetting.
- Ran `python -m compileall omicverse/external/latentvelo/utils.py` and `git diff --check`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5f1f81e7bc49`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.