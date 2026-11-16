# Issue

**Title:** Fix dimension plot point-size scaling

## Description

## Summary

- keep automatically sized non-raster dimension-plot points readable with square-root scaling and a `0.3` minimum
- scale raster point sizes with `raster.dpi` without rounding explicitly supplied `pt.size` values
- apply the same behavior to `CellDimPlot()` and `FeatureDimPlot()`

## Root cause

The previous automatic rule could shrink points below a readable size as cell counts increased. Raster point sizes were also rounded and did not scale with raster resolution.

## Validation

- `devtools::test(filter = "cell-dim-plot")`: 45 passed, 0 failed (one pre-existing ggplot2 deprecation warning)
- `git diff --check` passed

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3a77de132167`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.