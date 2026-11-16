# Issue

**Title:** Create staining.py

## Description

Apply stardist to segment cells from ssDNA figure.  The ssDNA figure is first splited into several small images before run stardist, because stardist can't satisfy large figure.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `41c46f0e3885`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.