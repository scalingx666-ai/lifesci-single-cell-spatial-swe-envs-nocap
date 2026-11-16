# Issue

**Title:** Fix ci

## Description

Only trigger PyPI publication action when we create a new release.
Update version checking regex to match PEP440.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `60f6a59c2086`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.