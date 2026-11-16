# Issue

**Title:** Add `ComplexHeatmap::pheatmap()` conversion option to `dittoHeatmap()`

## Description

A major goal here is to give users the ability to have large heatmaps be rasterized via that option (defualt for large heatmaps) within this package.
Additionally, allows users to take advantage of the extensive customizability offered by this package.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `74ffac7e35e2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.