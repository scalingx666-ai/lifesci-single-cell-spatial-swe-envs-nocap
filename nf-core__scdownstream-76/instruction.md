# Issue

**Title:** fix merge.py

## Description

- correct sample name splitting:
- do not update obs_names (they are already unique) 
- store a copy of X in layer (not a view)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e80004cce32b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.