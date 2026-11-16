# Issue

**Title:** Adata type check list

## Description

Support for tuple/list arguments that should have anndatas of a certain type.
Fixed calls to `check_adata_is_type` where `optional=True` were used for non-optional arguments.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b953e229e4db`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.