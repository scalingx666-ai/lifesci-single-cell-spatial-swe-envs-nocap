# Issue

**Title:** Build python 3.12 wheels

## Description

##### Issue
Wheels for Python 3.12 are missing.

##### Description of changes
- Updating workflow to build wheels for Python 3.12
- Removing building wheels for Python 3.7 which is already out-of-life

##### Includes
- [ ] Code changes
- [ ] Tests
- [ ] Documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8c62e662d974`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.