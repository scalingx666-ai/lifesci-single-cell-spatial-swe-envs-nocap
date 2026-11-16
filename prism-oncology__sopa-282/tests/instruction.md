# Issue

**Title:** Feat/min patch size parameter

## Description

Add a min patch size parameter (defaults to 10 pixels) to discard very small patches that could potentially break the pipeline.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `585dd0c62e90`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.