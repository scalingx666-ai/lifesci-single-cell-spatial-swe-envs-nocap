# Issue

**Title:** Marker search p-values

## Description

## P-Value Implementation 

### New Function:
- **`mannwhitneyu_from_ranks()`** - Vectorized Mann-Whitney U test with tie correction for rank-based marker identification

### Modified Functions:
- **`find_markers_by_rank()`** - Now calculates and returns p-values for all markers (added to output array)
- **`prenormed_mean_rank_wrapper()`** - Now calculates and returns p-values for prenormed data path
- **`DataStore.get_markers()`** - Output now includes `p_value` column

### Output Changes:
- **Marker results** now include 7 columns instead of 6:
  - `feature_index`, `score`, `mean`, `mean_rest`, `frac_exp`, `frac_exp_rest`, `fold_change`, **`p_value`** (new)
- **CSV exports** automatically include p-values

### Algorithm:
- Uses Mann-Whitney U test with tie correction via standard normal approximation
- ~~One-sided test (alternative='greater') for upregulated markers~~
- **Two-sided p-values**
- Handles zero-inflated scRNA-seq data properly

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `99ae5fcebf34`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.