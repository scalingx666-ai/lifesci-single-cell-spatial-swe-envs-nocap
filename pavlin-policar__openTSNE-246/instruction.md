# Issue

**Title:** Fix KL computation for dof != 1

## Description

This should hopefully fix #238 and in addition implement exact KL computation with arbitrary dof.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9f83ab6a87b7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.