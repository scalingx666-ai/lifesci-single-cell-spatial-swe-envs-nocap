# Issue

**Title:** Use all available distance metrics for nearest neighbors

## Description

##### Issue
Using only shared distance metrics is silly. We remove a lot of them just because the C++ implementation of VPTrees only support euclidean.

##### Description of changes
All metrics supported by each KNNIndex class are supported.

##### Includes
- [X] Code changes
- [X] Tests
- [ ] Documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8e1d33884bf0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.