# Issue

**Title:** Fixes #139

## Description

Deprecate neighbors_method attribute and replace it with neighbors to
satisfy scikit-learn warnings in repr.

##### Includes
- [X] Code changes
- [ ] Tests
- [ ] Documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8d65297a271e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.