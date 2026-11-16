# Issue

**Title:** Update the reference of pandas in `get_sz_exprs()` and `set_param_kinetic()`

## Description

Earlier code will fail with the pandas after 2.0.0.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a5c027d53343`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.