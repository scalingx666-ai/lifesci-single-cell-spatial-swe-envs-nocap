# Issue

**Title:** Debug ROC in LAP Shiny app

## Description

Bug description: ROC takes all transitions into consideration. It should only consider those with known transcription factors information.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a6b5e06b5220`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.