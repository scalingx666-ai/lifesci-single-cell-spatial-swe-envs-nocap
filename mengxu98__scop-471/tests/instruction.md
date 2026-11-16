# Issue

**Title:** Refactor CCC internals and split cccplot.R

## Description

## Summary

- Split all 107 helpers from `R/cccplot.R` by responsibility: 32 data and result helpers in `R/ccc-data.R`, 29 shared plotting helpers in `R/ccc-plot-utils.R`, and single-entry helpers in `R/CCCHeatmap.R` (10), `R/CCCNetworkPlot.R` (25), and `R/CCCStatPlot.R` (11).
- Remove `R/cccplot.R` after migrating its definitions. No helper function body, formal arguments, result shape, storage structure, or calculation order was changed.

## Reachability and retention basis

- Audited the current upstream source from `NAMESPACE` exports through package function calls and function-valued arguments, then checked direct and string-based references in CCC tests, examples, Rd files, and vignettes. Reviewed dynamic `do.call()` use and the evaluated plot call used for multi-method plotting.
- The repository-visible call graph reaches all 107 definitions. Therefore this PR removes no individual helper; the old file is removed only after its live functions are assigned to their owning files. This audit is limited to the repository and does not claim that external projects cannot use internal names.
- Parsed function ASTs before and after relocation: all 107 bodies match exactly, with no missing or duplicate definitions.

## Validation

- `Rscript -e 'pkgload::load_all(".", quiet=TRUE, compile=FALSE)'`: exit 0. It emitted the existing Windows startup locale and no-compile DLL warnings.
- CCC test set with `compile=TRUE`: unified build/update, backend parity, single/multiple-method plotting, comparisons, and spatial plotting passed. Four CRAN-guarded backend tests were skipped. `test-cccdb.R` had two namespace-state expectation failures after earlier tests loaded LIANA/tcltk and one Ensembl archive connection error; these do not touch the migrated plotting/data helpers.
- The requested `rcmdcheck` invocation reached Windows package installation but reported `Installation failed`; `rcmdcheck` then failed to decode the install output because it contained an embedded NUL. It did not reach `checking dependencies in R code` or the example dependency check, so those two check stages remain unverified in this environment.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `633c0cabc8e6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.