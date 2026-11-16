# Issue

**Title:** version 1.9.20 (2020-02-16)

## Description

Fix bug in handling of tail probability tests such that
Epsilon*=0 was not handled correctly and all probabilities
were reported as exactly 1.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e0617f5adad6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.