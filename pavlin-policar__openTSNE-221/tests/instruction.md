# Issue

**Title:** Fix inplace optimization changing init (in some cases)

## Description

##### Issue
In some forms of usage, the initialization was changed, which is incorrect.


##### Description of changes
Copy the intialization when constructing `TSNEEmbedding` and `PartialTSNEEmbedding` objects. This only happens once, so the memory impact should be minimal.

##### Includes
- [X] Code changes
- [X] Tests
- [ ] Documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5d829feae25d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.