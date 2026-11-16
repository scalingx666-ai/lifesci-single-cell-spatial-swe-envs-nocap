# Issue

**Title:** Parquet-based dataset creation

## Description

- Changed dataset creation to work with parquet files (only) and be blazing fast 🔥 🔥 🔥 
- Added possible support for MERSCOPE and other spatial technologies through settings YAML files.
- Tested on existing training and prediction steps.
- Updated CLI to use new dataset creation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a619d3f6d94c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.