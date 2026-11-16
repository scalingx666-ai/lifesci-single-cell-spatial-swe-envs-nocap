# Issue

**Title:** Add and fix docstrings in core/_anndata.py

## Description

## Changes and bug fixes

* Fix minor issues in docstrings (missing documentation, inconsistent argument names) in `clean_obs_names`, `get_df`, `merge` and `show_proportions`.

## New

* Add docstrings to `get_initial_size`, `get_size`, `obs_df`, `set_initial_size`, `var_df` and `verify_dtypes`.

## Related issues

Contributing to #406.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `595b47d7fa0f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.