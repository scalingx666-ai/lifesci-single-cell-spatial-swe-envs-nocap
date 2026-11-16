# Issue

**Title:** Refactor clean_obs_names

## Description

## Changes

* Renames input arguments `data` to `adata`, `copy` to `inplace`, `ID_length` to `id_length`, `base` to `alphabet`
* Uses Pandas functionality
* Uses regex expression to extract new observation names
* Renames variables to be more meaningful and be snake as well as lower case

## Related issues

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ab5234c9fe97`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.