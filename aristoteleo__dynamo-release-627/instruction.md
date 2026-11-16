# Issue

**Title:** Debug `classify_clone_cell_type()`

## Description

Bug description: Existing implementation outputs the index of excluded cell type instead of the dominant cell type in a given clone.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e87f702da0eb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.