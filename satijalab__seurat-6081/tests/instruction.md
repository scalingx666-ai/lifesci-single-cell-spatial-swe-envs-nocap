# Issue

**Title:** Fix/PlotPerturbScore

## Description

Made a small change to fix #5134.
The issue was the cell name structure and how we were pulling those names inside `PlotPerturbScore`. Hopefully this new version will be more flexible to different cell name structures.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b5b553b8948c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.