# Issue

**Title:** Fix typo in vignette

## Description

Using just `group` will match multiple arguments and thus fail.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `963d32474b93`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.