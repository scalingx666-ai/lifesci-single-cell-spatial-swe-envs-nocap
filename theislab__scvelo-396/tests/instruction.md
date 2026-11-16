# Issue

**Title:** Move functions to core/_anndata.py

## Description

## Changes

Functions related to or performing operations on AnnData, are moved to `core/_anndata.py`.
* Functions moved from `preprocessing/utils.py`: `cleanup`, `get_initial_size`, `get_size`, `set_initial_size`, `show_proportions`, `verify_dtypes`. 
* Functions moved `read_load.py`: `clean_obs_names`, `get_df`, `merge`, `obs_df`, `var_df`.

## Related issues

Related to #389.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9048768724c2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.