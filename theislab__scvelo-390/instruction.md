# Issue

**Title:** Move parallelize machinery to core

## Description

## New

* The file `core/_parallelize.py` is added

## Changes

* The functions `_parallelize` and `get_n_jobs` are moved to `core/`
* The function `_parallelize` is renamed to `parallelize`.

# Related issues

Related to #389.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8042371fb4f6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.