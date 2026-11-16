# Issue

**Title:** Update utils.py to fix issue with find_markers()

## Description

Current find_markers() command triggers multi-dimensional indexing by numpy which was depreciated in numpy 1.23.

Current fix flattens expr_frac to avoid this

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `286da4ad22a9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.