# Issue

**Title:** Backport PR #3987 on branch 1.5.x (fix(data): retry transient connection errors when downloading built-in datasets)

## Description

Backport PR #3987: fix(data): retry transient connection errors when downloading built-in datasets

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6de0d523a309`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.