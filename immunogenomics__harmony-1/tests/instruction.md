# Issue

**Title:** Cran

## Description

This reverts all floats back to doubles in the Rcpp code. Default RBlas does not have functions for float types.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ad4e75cbc71c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.