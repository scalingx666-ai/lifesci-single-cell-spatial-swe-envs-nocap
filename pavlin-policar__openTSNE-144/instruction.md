# Issue

**Title:** Update to annoy v1.17.0

## Description

##### Description of changes
Update annoy dependency to v1.17. This should be faster than before, as index building now uses multiple cores. 

##### Includes
- [X] Code changes
- [ ] Tests
- [ ] Documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1a1172dabcaa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.