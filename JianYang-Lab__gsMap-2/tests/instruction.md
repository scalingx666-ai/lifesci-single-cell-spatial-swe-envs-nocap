# Issue

**Title:** fix divide zero in `compute_regional_mkscore`

## Description

changed all small entries in `focal_whole` to 1 to avoid divided by zero error.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2d54a1dc132d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.