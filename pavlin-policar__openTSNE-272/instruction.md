# Issue

**Title:** Fix issue with BH being slower on multithreading

## Description

##### Issue
.


##### Description of changes
In Cython 3, marking functions as nogil does not actually make them `nogil`. The correct signature is `except nogil`. This commit updates the function signatures to this new specification. Nothing changes, as this was implicitly assumed in previous versions of Cython.

##### Includes
- [X] Code changes
- [ ] Tests
- [ ] Documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `80d4f3dc4b8a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.