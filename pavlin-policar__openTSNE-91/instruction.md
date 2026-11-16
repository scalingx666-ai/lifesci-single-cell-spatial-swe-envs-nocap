# Issue

**Title:** Build sdist on separate linux vm

## Description

##### Issue
In #90, it was brought up that the current azure-pipelines setup somehow doesn't properly package the source distribution, and doesn't include *.pxd or *.c files, as well as ignores the fftw matrix_mul implementation.


##### Description of changes
Package sdist on a separate unix VM.

##### Includes
- [X] Code changes
- [ ] Tests
- [ ] Documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cedb5144c526`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.