# Issue

**Title:** Audit Suggests usage and exported help topics

## Description

## Summary

Remove unused `Rfast` from Suggests after checking package code, tests, vignettes, examples, native sources, build scripts, and CI. Retain dependencies with actual uses, including BiocParallel, withr, and RcppParallel. All 347 direct exports have help aliases and all 353 help pages have titles, so no title additions are needed.

Keep the database species-alias regression independent of optional GSVA: exercise grouped and single-cell scoring with native ssGSEA. The sparse z-score path queries the GSVA version for compatibility and caused the newly added upstream test to fail on hard-dependency CI installations. The replacement preserves all alias, species-metadata, and combined-database assertions; it does not skip tests, change runtime code, or add a dependency.

## Validation

- DESCRIPTION parsing, help alias/title audit, and `git diff --check` pass.
- The full species-compatibility test file passes with `gsva_standardize()` replaced by a test-only error, proving the fixture does not enter the optional GSVA version path.
- `pkgload::load_all(".", quiet = TRUE, compile = FALSE)` passes.
- Previous local package checks identified pre-existing local thisplot/thisutils export warnings and the RunSingleR argument-documentation warning. Exact CRAN incoming checks encountered network failures; these are not claimed as successful checks.
- Updated cross-platform CI validates the final branch.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `633c0cabc8e6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.