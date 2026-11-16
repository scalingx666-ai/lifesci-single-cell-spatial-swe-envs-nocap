# Issue

**Title:** Keep the same index in geo_df and table before filtering cells

## Description

Fix #409

- parse the table/geo_df before filtering
- if aggregating genes and channels, ensure they have the same index before adding to obsm
- raises an error if all cells were filtered, and ensures the filter column if removed before the error so that we can re-run the aggregation right after

FYI @alihamraoui

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `132e1041cc79`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.