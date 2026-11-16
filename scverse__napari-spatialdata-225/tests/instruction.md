# Issue

**Title:** simplify conditional

## Description

This simplifies the conditional when looking for a layer that has `_columns_df` in the metadata and also fixes issues when looking for a layer that has sdata but not name in the metadata.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `07111f57f2fd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.