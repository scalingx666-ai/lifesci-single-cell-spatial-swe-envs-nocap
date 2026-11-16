# Issue

**Title:** Redesign ClusterTreePlot layout and legends

## Description

## Summary

- redesign `ClusterTreePlot()` with a bottom-anchored, collision-aware tree that expands from the starting side
- add `direction` support for left-to-right, right-to-left, top-to-bottom, and bottom-to-top trees
- add `label.fg = "auto"` with per-node WCAG contrast selection between black and white labels
- replace the crowded edge legends with a compact two-sample `Cells moved` linewidth guide and an `Incoming share` colour bar
- make `legend.position = "auto"` non-overlapping by construction: horizontal trees place a compact guide row above the panel, aligned to the starting side, while vertical trees place guides on the right
- retain `legend.position = "inside"` only as an explicit force-in-panel option
- make plot text and axes Arial/black by default, remove the redundant default title and panel border, and retain explicit overrides
- preserve multi-feature guide content with patchwork and synchronize the generated Rd documentation
- require ggplot2 >= 3.5.0 for the supported inside-legend API

## Validation

- `Rscript -e 'pkgload::load_all(".", quiet=TRUE, compile=FALSE)'`
- `Rscript -e 'pkgload::load_all(".", quiet=TRUE, compile=FALSE); testthat::test_file("tests/testthat/test-cluster-tree-plot.R", reporter="summary")'`
- ragg PNG visual QA at 720 x 604 for the default single-feature tree
- ragg PNG visual QA for a sparse 2-3 resolution tree, two-feature patchwork output, and all four tree directions
- 2 x 2 direction QA confirms legends remain outside every data panel without covering nodes or edges
- verified multi-feature patchwork grobs retain the shared and feature guide content
- `_R_CHECK_FORCE_SUGGESTS_=false Rscript -e 'rcmdcheck::rcmdcheck(args=c("--no-manual","--as-cran","--no-examples","--no-tests"), error_on="never")'`
  - 0 errors
  - 2 warnings and 4 notes from pre-existing, untouched CellRank/other Rd/DESCRIPTION issues
  - `checking dependencies in R code ... OK`
  - `checking for unstated dependencies in examples ... OK`
  - `checking for unstated dependencies in 'tests' ... OK`

## Notes

- No optional/Remotes backend calls, environment guards, or global options were added.
- CI status is pending after the latest push.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2bfa19c6e6b7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.