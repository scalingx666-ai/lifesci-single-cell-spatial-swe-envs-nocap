# Issue

**Title:** Save velocity parameters to .varm instead .var

## Description

Use a matrix called `vel_params` in `.varm` to replace all velocity parameters in `.var`. Column names will be saved in `.uns` as `vel_params_names`.  Cell-wise velocity will remain the same. Helper functions to read and update the parameters are created.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `153f5b7c84b7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.