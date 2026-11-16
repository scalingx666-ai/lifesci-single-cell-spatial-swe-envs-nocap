# Issue

**Title:** Fix single-feature GroupHeatmap aggregation

## Description

`GroupHeatmap()` produces a blank heatmap and loses the gene label when `features` contains one gene. In the mean-expression and expression-fraction paths, `vapply()` simplifies a single-feature result to a vector; the subsequent aggregation layout transposes and recycles it incorrectly.

Restore an explicit genes-by-groups matrix before applying the existing layout. Regression tests cover one or multiple groups, unused factor levels, split heatmaps, agreement with the corresponding multi-gene row, and flipped dot heatmaps.

Validation:

- The new aggregation assertions fail on the original implementation and pass with the fix.
- All 50 assertions in the GroupHeatmap and heatmap row-label tests pass without warnings or skips.
- A synthetic 9-cell-type, 4-group example reproduces the original blank plot. The corrected single-gene plot retains `Rpsa` and matches the multi-gene control numerically.
- `pkgload::load_all(".", quiet=TRUE, compile=FALSE)` passes.

- `_R_CHECK_FORCE_SUGGESTS_=false` with `rcmdcheck::rcmdcheck(args=c("--no-manual", "--as-cran", "--no-examples", "--no-tests"), error_on="never")` completes with **0 errors, 1 warning, 7 notes**. Both `checking dependencies in R code` and `checking for unstated dependencies in examples` are **OK**. Validation used R 4.4.1, thisutils 0.5.3 and thisplot 0.4.6.

The sole package-check warning concerns loading the existing `visium_human_pancreas_sub` dataset (`unable to find required package 'Seurat'`). R's native dataset checker reproduces the warning on clean upstream commit `2f44f8c` in the same environment.

The full test suite was interrupted after an unrelated ATAC scDblFinder `findKNN` failure for `dgCMatrix`. The same failing test was independently reproduced on that clean upstream commit in this environment; a full-suite pass is not claimed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2f44f8c52c24`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.