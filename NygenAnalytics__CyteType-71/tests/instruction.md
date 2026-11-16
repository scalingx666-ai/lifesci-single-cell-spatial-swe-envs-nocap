# Issue

**Title:** Update version to 0.19.2 and enhance metadata handling in CyteType

## Description

- Bump package version to 0.19.2.
- Introduce max_metadata_categories parameter to limit unique values in categorical obs columns during cluster metadata aggregation, improving memory efficiency.
- Increase maximum upload size for obs_duckdb from 100MB to 2GB, accommodating larger datasets.
- Refactor save_obs_duckdb function to ensure proper cleanup of temporary columns after processing.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `98cbecdae71c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.