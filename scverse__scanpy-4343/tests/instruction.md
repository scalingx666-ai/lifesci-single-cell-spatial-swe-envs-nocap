# Issue

**Title:** Backport PR #4342 on branch 1.12.x (ci: fix autofix workflow)

## Description

Backport PR #4342: ci: fix autofix workflow

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cc4c0904379c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.