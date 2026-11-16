# Issue

**Title:** Partial bugfix avoiding re-rendering of `ComplexHeatmapPlot` panel wh…

## Description

…en incoming selection changes if custom rows are in use.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f585c8cac455`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.