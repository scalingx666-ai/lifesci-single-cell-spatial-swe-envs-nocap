# Issue

**Title:** Alternative solution to #590

## Description

Deprecates PR #590

Achieves the same result using only one new generic instead of two.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7b1452fed0b4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.