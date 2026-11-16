# Issue

**Title:** fix: reuse RCTD weights in SpaTalk

## Description

﻿## Summary
- make SpaTalk preflight accept working installed `SpaTalk`/`NNLM` packages even when GitHub remote metadata is absent, while retaining the official-repository fallback
- add `deconvolution = "RCTD"` to reuse `srt@tools[[rctd.tool]]$weights` and pass imported weights to official SpaTalk method 2
- validate/reorder spot weights, validate cell-type compatibility, and record deconvolution provenance without storing the matrix in backend arguments
- update Rd/NEWS and add focused regression tests

## Validation
- `Rscript -e "pkgload::load_all('.', quiet=TRUE, compile=FALSE)"`
- focused `tests/testthat/test-run-spatalk.R`: 108 expectations passed
- `tools::Rd2ex('man/RunSpaTalk.Rd')` + `parse()`: passed
- live official SpaTalk 1.0 STARmap spot/reference run using stored RCTD-like weights: 132 spots, 14 cell types, 3 LR rows, 3 TF rows; stored coefficients identical to supplied weights
- `_R_CHECK_FORCE_SUGGESTS_=false R CMD check --as-cran --no-manual --no-examples --no-tests`: 0 errors; `checking dependencies in R code ... OK`; `checking for unstated dependencies in examples ... OK`

The remaining check warning is pre-existing and comes from direct `infercnv`/`numbat` references in unrelated tests. No optional backend was added to Imports/Depends/Suggests.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `45811b678fe1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.