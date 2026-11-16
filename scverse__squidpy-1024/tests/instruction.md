# Issue

**Title:** chore: fix messed-up yaml formatting

## Description

Using 4 with prettier is not compatible how `-` lists work, which leads to weird indenting that isn’t a multiple of 4 and is therefore hard to edit.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `32789aefd53b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.