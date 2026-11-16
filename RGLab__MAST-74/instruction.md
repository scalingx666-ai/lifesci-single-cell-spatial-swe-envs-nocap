# Issue

**Title:** Merge missing changes from Bioc/master to origin master via diff patches

## Description

I created a diff patch between bioc/master and origin/master and applied it.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4aefa6f3dd95`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.