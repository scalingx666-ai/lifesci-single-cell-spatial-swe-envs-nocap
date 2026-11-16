# Issue

**Title:** use zinb for everything in vi

## Description

NB can be modeled as ZINB with 0 dropout probability, which can be used to simplify the code.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d49872e79ece`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.