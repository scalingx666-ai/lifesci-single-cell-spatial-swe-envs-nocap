# Issue

**Title:** fix: disable FE auth testing on compatibility tests

## Description

Disable the frontend auth testing for compatibility tests as they are breaking, and we don't run auth on explorer anymore.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `660dff256c3c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.