# Issue

**Title:** Add CellPhoneDB Method 3 support

## Description

## Summary

- add `method=2` / `method="statistical"` and `method=3` / `method="degs"` dispatch to `ov.single.run_cellphonedb_v5`
- require and forward `degs_file_path` for Method 3 while keeping Method 2 as the default
- adapt Method 3 `relevant_interactions` into communication AnnData without treating DEG relevance as a statistical p-value
- make stored CellPhoneDB result tables H5AD-safe, including mixed object columns and absent CellSign outputs
- apply the existing duplicate-gene scoring compatibility fix to both CellPhoneDB methods

## Plot semantics

Method 3 results carry a boolean `relevance` layer and `support_kind="relevance"`. Filtering uses that layer directly, independent of `pvalue_threshold`. P-value coloring is rejected for Method 3 because CellPhoneDB does not calculate statistical p-values for DEG relevance. A binary compatibility `pvalues` layer is retained only for legacy consumers.

## Validation

- `12 passed`: focused Method 2/3 dispatch, adapter, H5AD round-trip, and scoring compatibility tests
- `133 passed`: full `tests/pl/test_ccc_plots.py` regression suite
- real end-to-end Method 3 run with the official CellPhoneDB tutorial data and database, including interaction scoring across all 42 cell types
- real result: communication AnnData shape `(1764, 2010)`, with 18,544 relevant entries
- real H5AD write/read round trip passed

Official validation data: https://github.com/ventolab/CellphoneDB/blob/master/notebooks/data_tutorial.zip

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `16f3d8f20f3c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.