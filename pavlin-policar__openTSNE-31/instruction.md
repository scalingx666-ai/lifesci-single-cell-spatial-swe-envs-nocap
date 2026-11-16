# Issue

**Title:** Remove openmp flag for mac sytems

## Description

##### Issue
The library can't be properly compiled on Macs because the default compiler `clang` doesn't support `openMP`.

##### Description of changes
Disable openMP for the time being.

##### Includes
- [X] Code changes
- [ ] Tests
- [ ] Documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1966261236d5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.