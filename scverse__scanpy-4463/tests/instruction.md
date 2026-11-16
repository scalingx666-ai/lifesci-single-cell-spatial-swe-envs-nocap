# Issue

**Title:** ci: pin python for benchmarks

## Description

Otherwise 3.12 is used which doesn’t support the current minimum

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1a421f222c65`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.