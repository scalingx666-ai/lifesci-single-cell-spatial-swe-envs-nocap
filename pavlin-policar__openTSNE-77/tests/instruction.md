# Issue

**Title:** Lazily import pynndescent

## Description

##### Issue
Numba is a bit slow to load, and if we use exact neighbors, than it's being loaded for no reason.


##### Description of changes
Only load pynndescent and, consequently, numba, when using approximate neighbors.


##### Includes
- [X] Code changes
- [ ] Tests
- [ ] Documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `87f8b7b30aa2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.