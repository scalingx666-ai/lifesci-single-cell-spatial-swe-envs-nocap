# Issue

**Title:** Make registration_pseudobulk compatible with pseudobulkDGE workflow

## Description

- Preserve `var_registration` original column in the sce_pseudo, prevents make syntatic changes to the original variable 
- Add `filter_expr` as variable to filter genes or not, keep default TRUE (for pseudoblkDGE the filtering is group specific)
- Add "pseudo" QC variables `pseudo_sum_umi`, `pseudo_expr_chrM`, `pseudo_expr_chrM_ratio` (user must provide `mito_gene` vector to indicate mitochondrial genes and calc mito variables)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1de5729661ff`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.