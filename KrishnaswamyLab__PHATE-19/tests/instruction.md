# Issue

**Title:** Fix pypi again

## Description

Loading README.rst in setup.py needs to be outside the call to `setup`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4d613622753b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.