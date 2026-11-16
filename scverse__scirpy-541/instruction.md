# Issue

**Title:** GPU implementation of hamming distance

## Description

Hamming distance implementation with numba.cuda for GPU support.
This is built on top of the changes in Hamming distance implementation with Numba #512

@grst:
- [x] add to API docs
- [x] start small "large dataset tutorial",  
- [x] update changelog

Close #479

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4157ae484585`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.