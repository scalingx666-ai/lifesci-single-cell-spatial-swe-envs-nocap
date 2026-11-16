# Issue

**Title:** Add small cluster extraction to quantile_align_SNF

## Description

Also save SNF in class slot, only recompute when parameters
change. Clean up text output of quantile_align_SNF.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a96ede1ae3c2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.