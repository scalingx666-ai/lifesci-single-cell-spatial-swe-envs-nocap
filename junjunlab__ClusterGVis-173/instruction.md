# Issue

**Title:** Add legacy argument compatibility

## Description

﻿## Summary

Adds a small compatibility layer for legacy argument names that are still used in older examples and issue reports.

- maps `getClusters(exp = ...)` to `obj`
- maps `clusterData(exp = ..., cluster.method = ..., cluster.num = ...)` to the current argument names
- maps common old `visCluster()` dotted arguments such as `plot.type`, `markGenes.side`, `annoTerm.data`, `line.side`, `cluster.order`, `go.col`, and `add.bar`
- filters `show_column_names` / `show_row_names` before forwarding arguments to `ComplexHeatmap::Heatmap()` to avoid duplicate-argument errors

This addresses the legacy-argument failures discussed in issues #160, #167, #168, #169, #170, and #171.

## Validation

- `Rscript -e "setwd('ClusterGVis'); devtools::load_all('.'); testthat::test_dir('tests/testthat')"`
  - Result: 0 failures, 21 passes
  - Existing warnings remain for deprecated test helpers (`ggplot2::is.ggplot()` and `testthat::expect_is()`).

`R CMD check .\\ClusterGVis --no-manual --no-build-vignettes` was also attempted, but it stops before running code because the current DESCRIPTION is missing generated `Author` / `Maintainer` fields from the checker perspective. That metadata issue appears unrelated to this change.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c852fe735a0c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.