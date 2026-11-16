# Issue

**Title:** Pydicom update

## Description

Security issue flagged in https://github.com/Dana-Farber-AIOS/pathml/security/dependabot/27

Update means PathML will not be compatible with Python 3.9 anymore.

Adding Python 3.11 and 3.12 to test suite.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7a303aae0e54`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.