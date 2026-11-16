# Issue

**Title:** Move NNLM to suggested instead of required

## Description

This is to allow for easier installation as NNLM was recently removed from CRAN.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5a1b22406961`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.