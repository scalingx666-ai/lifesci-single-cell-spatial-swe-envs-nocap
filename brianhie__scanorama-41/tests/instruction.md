# Issue

**Title:** Move random seed into correct and integrate functions

## Description

Real fix to issue 

Use same random seed on each call to `correct()` and `integrate()` and let user specify it

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `26d60b40bc88`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.