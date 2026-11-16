# Issue

**Title:** fix(single): validate cNMF result mapping

## Description

## Summary

Fixes cNMF result mapping so `get_results()` and `get_results_rfc()` validate and align results by AnnData cell names before writing cNMF usage and gene scores back to `adata`.

- Adds shared cNMF result alignment validation for cell and gene indices
- Prevents silent NaN or misleading mappings when `adata.obs_names` do not match `usage_norm.index`
- Preserves correct behavior when `adata` is reordered or subsetted by matching cell names
- Removes the duplicate dead `get_results_rfc()` definition
- Adds regression tests for reordered cells, missing cells, and repeated mapping calls

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `77f3a4e6306f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.