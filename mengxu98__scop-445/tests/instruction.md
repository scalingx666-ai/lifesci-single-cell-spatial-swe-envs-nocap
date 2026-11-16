# Issue

**Title:** fix: align abundance tests and method-specific plots

## Description

## Problem

The differential-abundance workflow exposed Milo neighborhood results without projecting them through neighborhood cell membership. Its common plotting rule also treated scCODA credibility as frequentist FDR, and Milo neighborhood significance used ordinary BH FDR ahead of SpatialFDR. Sample-level methods collapsed or failed when donor IDs recurred across conditions, permutation ignored the public `seed`, and automatic virtual samples could yield apparently inferential p-values without biological replicates.

## Changes

- Project Milo neighborhoods onto their stored member cells for discrete and continuous UMAP views. Overlapping significant directions are marked `Mixed`; cells without a neighborhood are `Uncovered`. Effect plots identify Milo neighborhoods and log2 FC explicitly.
- Use scCODA's stored credibility decision for scCODA plots and `SpatialFDR` for Milo neighborhood results, retaining ordinary BH FDR separately as `BH_FDR`.
- Preserve sample-condition units. Fully paired donor IDs use paired sample-proportion tests and paired bootstrap intervals; Milo R/C++ designs include donor blocking. Partially paired comparisons fail with a clear message. Store Milo sample mappings.
- Honor `seed` in permutation testing.
- Require biological `sample.by` for Milo, scCODA, and the internal Propeller-style method by default. `allow_pseudo_samples = TRUE` is an explicit descriptive mode; p-values, FDR, credibility and inferential intervals are unavailable in its exposed results.
- Clarify method provenance in plots, documentation, and NEWS; synchronize Rd files. Make the scCODA Python helper test choose a working interpreter on Windows.

## Validation

- `pkgload::load_all(".", quiet=TRUE, compile=FALSE)` passed.
- Four focused test files: 59 assertions passed, including public plot calls and a real Milo C++ paired-donor call.
- Windows `R CMD check --no-manual --as-cran --no-examples --no-tests` completed using a D: temporary directory and `C` locale. `checking dependencies in R code ... OK` and `checking for unstated dependencies in examples ... OK`. Final status: one existing `RunSingleR.Rd` argument-documentation WARNING and three unrelated repository/environment NOTEs.
- Synthetic neighborhood effect and UMAP plots were exported and visually checked.

## Remaining validation limits

`miloR` is unavailable in the local R library, so its R backend was checked against the official `countCells()` / `testNhoods()` API but was not run locally. A live scCODA MCMC environment is also unavailable; Python helper behavior and stored-result plots were tested. CI results for this PR should be reviewed before merge.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `59e0fb19292e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.