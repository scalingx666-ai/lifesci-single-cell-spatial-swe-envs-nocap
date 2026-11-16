# Issue

**Title:** Bug fixes and improvements

## Description

- Fix error in Python 3 with hvg=None
- Expose knn parameter
- Bug fix in way hvg genes were being determined

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e4f2c6802ff3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.