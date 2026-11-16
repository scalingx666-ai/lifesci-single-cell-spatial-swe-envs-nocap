# Issue

**Title:** Remove constant 4 factor from gradients

## Description

##### Issue


##### Description of changes
Remove constant factor from gradients. This deviates from the true gradient and the implementation in scikit-learn, but is now consistent with FIt-SNE and van der Maaten's implementation.

##### Includes
- [X] Code changes
- [ ] Tests
- [ ] Documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ee29af7b83d9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.