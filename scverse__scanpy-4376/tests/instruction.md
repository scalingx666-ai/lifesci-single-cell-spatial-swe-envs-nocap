# Issue

**Title:** Backport PR #4298 on branch 1.12.x (fix: don't warn from log1p about X when transforming a layer or obsm)

## Description

Backport PR #4298: fix: don't warn from log1p about X when transforming a layer or obsm

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e15ff3f98fe9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.