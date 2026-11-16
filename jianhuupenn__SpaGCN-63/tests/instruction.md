# Issue

**Title:** Replace sklearn with scikit-learn dependency

## Description

The sklearn package is dead and does not exist anymore. Long live scikit-learn.

This fixes major installation issues.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0f265b80ff75`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.