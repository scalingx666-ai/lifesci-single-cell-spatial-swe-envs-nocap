# Issue

**Title:** Fix wrong normalization for affinities in fixed sigma affinities

## Description

##### Issue
For some reason, the affinity matrix in for fixed sigmas wasn't normalized properly.


##### Description of changes
Properly normalize.

##### Includes
- [X] Code changes
- [ ] Tests
- [ ] Documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5899b2ff263e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.