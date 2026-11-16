# Issue

**Title:** Remove VPTree and move query_train into build index function

## Description

##### Issue
When using `pynndescent` for approximate NN search, the index was built, then queried with the training data. Little did I know that I could get the nearest neighbors out of the index as soon as it was built.

##### Description of changes
Properly use pynndescent when querying nearest neighbors for training data.

##### Includes
- [X] Code changes
- [ ] Tests
- [ ] Documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a82b7b42c65f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.