# Issue

**Title:** Set dev version

## Description

- Update `main` to contain all commits from `cran`, plus:
  - README is updated to show v6
  - dev version (.9xxx) is set for future PRs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ac3e96038065`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.