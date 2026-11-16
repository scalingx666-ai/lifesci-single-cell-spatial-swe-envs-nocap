# Issue

**Title:** Improvements in make_bulk

## Description

Rewrote `make_bulk` method of `DataStore` to support:
- pseudobulking using either raw or normalized counts
- When bulking using raw counts the values from cells are summed while when using normalized data, mean of values across the cells is calculated.
- Added ability for secondary grouping
- Added calculation of fraction of cells expressing features.
- Improved handling of the output dataframe indices

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5e5f219ff08c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.