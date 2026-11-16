# Issue

**Title:** feat: label_insitu now defaults to TRUE in dim plots

## Description

## Summary

`label_insitu` now defaults to `TRUE` in `CellDimPlot()`, `FeatureDimPlot()`, `PAGAPlot()`, and the CCC embedding-network plots, so `label = TRUE` shows group names (or cluster IDs) directly on the plot instead of renumbered labels that must be matched through the legend. Previously `seurat_clusters` 0-based IDs were silently renumbered to 1-k, producing confusing legend entries like `1: 0`.

- Redundant `label_insitu = TRUE` removed from roxygen examples and two vignettes.
- `label_insitu = FALSE` restores the previous numbered-label behavior; documented in NEWS.
- The earlier trend-fitting refactor commits on this branch were dropped: they were already merged to main via #450.

## Test notes

- `testthat`: cell-dim-plot + cell-scoring-plot suites on the rebased branch — 220 pass / 0 fail / 0 warnings.
- Visual comparison on the built-in `pancreas_sub` (`seurat_clusters` and `CellType` UMAPs) confirms in-situ labels match the legend IDs after the default change.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1d7d9fb7976d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.