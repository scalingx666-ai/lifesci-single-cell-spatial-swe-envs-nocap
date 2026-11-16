# Issue

**Title:** Fix compilation flags on Windows

## Description

The module was not being properly compiled on Windows, the `openmp` and `O3` flags aren't' the same on Windows. This resulted in the library being slower on Windows than scikit-learn ()!

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5ffbdaa0db0e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.