# Issue

**Title:** Backport PR #4075 on branch 1.5.x (fix(scbasset): compute training AUROC on CPU when the model is on MPS)

## Description

Backport PR #4075: fix(scbasset): compute training AUROC on CPU when the model is on MPS

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `786956892ed6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.