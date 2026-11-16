# Issue

**Title:** Backport PR #4087 on branch 1.5.x (fix(distributions): stabilize float32 NB gradient with respect to mu)

## Description

Backport PR #4087: fix(distributions): stabilize float32 NB gradient with respect to mu

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `857385851ef0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.