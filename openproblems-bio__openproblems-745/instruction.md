# Issue

**Title:** Prevent pip install conflicts

## Description

Installing things in separate lines leads to accidental conflicts. This prevents that (mostly).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `becb1f6fe35a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.