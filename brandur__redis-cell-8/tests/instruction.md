# Issue

**Title:** Fix Travis

## Description

Migrates CI release system to trust:

https://github.com/japaric/trust

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8d13fca32311`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.