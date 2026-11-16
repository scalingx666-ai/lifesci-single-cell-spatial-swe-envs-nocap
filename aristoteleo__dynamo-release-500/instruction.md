# Issue

**Title:** Update Reorganize pp

## Description

Fixed a few issues in reorganizing preprocessing:

- add `_legacy `to every deprecated function.
- remove extra `__init__ `file in the root folder.
- add support for `normalize_cell_expr_by_size_factors `.
- solve a few bugs and wrong import statements related to preprocessing.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2c0aa136e9ff`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.