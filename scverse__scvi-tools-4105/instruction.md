# Issue

**Title:** Backport PR #4102 on branch 1.5.x (ci: switch from pre-commit.ci to autofix.ci)

## Description

backports #4102 as requested:

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a03af8b7d835`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.