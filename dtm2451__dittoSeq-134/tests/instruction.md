# Issue

**Title:** Additional data representation controls for dittoPlot and related plotters

## Description

Adds additional control to how data representations requested via the`plots` inputs can be shown.  Specifically:
- `boxplot.outlier.size` (passed to `geom_boxplot(outlier.size)`), per #133 
- `vlnplot.quantiles` (passed to `geom_violin(draw_quantiles)`)

ToDo before merge:
- [x] double-check documentation
- [x] add unit tests

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2ce709d87cf2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.