# Issue

**Title:** Fix NaN values in adata.obs

## Description

NOTE: 

- for scanpy's rank genes marker search, 'nan' clusters are dropped, i.e no marker genes
- Changed current fix to raise error when there are nan values in the group_key column and can flag drop=True to proceed with dropping cells without the cluster labels
- cytetype marker detection raises error if nan, so that is accounted for 

## NaN handling for cluster labels in `adata.obs[group_key]`

- `validate_adata` now checks for NaN values in the group key column before any downstream processing
- **Default behavior:** raises a `ValueError` with the count and percentage of affected cells, guiding the user to either fix their data or opt into dropping
- **With `drop_na_cells=True`:** drops NaN cells in-place with a warning and proceeds with annotation
- Always raises if all cells are NaN, regardless of the flag
- Added `drop_na_cells` parameter to `CyteType.__init__`, passed through to `validate_adata`

### Files changed

- `cytetype/preprocessing/validation.py` — NaN detection and handling in `validate_adata`
- `cytetype/main.py` — `drop_na_cells` parameter on `CyteType.__init__`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e27bd80a4ff3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.