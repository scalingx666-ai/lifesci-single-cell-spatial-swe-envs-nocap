# Issue

**Title:** Remove duplicate size factors calculation

## Description

Debug the problem that the preprocessing module still calculates the size factors twice. After modification, `normalize()` only calculates the size factors when it can't detect existing ones.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e5e9017f84ed`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.