# Issue

**Title:** Debug average in `fate()`

## Description

Bug description: 

- The average option is disabled in the fate(). 
- It doesn't distinguish the "origin" and "trajectory mode" as described in the docstring.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e87f702da0eb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.