# Issue

**Title:** feat(atac): add regional insertion matrices and plots

## Description

## Scope
Independent feature-scoped draft requested by the user: `RunATACRegionMatrix()`, `ATACRegionHeatmap()` and `ATACRegionPlot()`: explicit endpoint tabulation, orientation, duplicate endpoints, bounded allocation and normalization. No genome-tiles interface in this branch.

Based on current main `2f44f8c52c247c5a5b42a8a2cb3a7c9800ae24cb`; does not include or alter #528/#529 or sibling new ATAC interfaces. No interactive genome browser.

## Verification
- Recovered checksum-verified source, split into an independent branch.
- `git diff --cached --check` passes; private helpers and tests are scoped independently.
- Published tree matches prepared local tree `1b771828bc8074e91cf684930fffa565fba06008` exactly.
- Historical combined implementation evidence: Actual indexed-fragment, duplicate-endpoint, bin-boundary and plot normalization tests. Explicit SCOP endpoint semantics, not claimed identical to native Signac RegionMatrix. These prior results are NOT fresh split-branch validation.
- Fresh installed-package focused validation has now completed; see the exact-head results below. Hosted CI is reported separately and this remains a draft.

## Boundaries
Synthetic/native parity is software acceptance, not biological validation. Optional dependencies and external resource limitations remain explicit; APIs do not install packages or download reference data. No merge is requested or performed.

## Fresh exact-head validation (2026-11-01)
Head `407d04bde207d55fdaccf6c90ba58746b2eabf5a`, tree `1b771828bc8074e91cf684930fffa565fba06008`: independent package installation and installed-export isolation verified. Focused tests: **27 passing expectations, 0 failures, 0 errors, 0 skips, 1 visible upstream deprecation warnings**. R4.5.3 / Signac1.17.1 / Seurat5.5.1 / testthat3.3.2. All branch R/test/Rd source parses. Full tracked snapshot blobs match this published tree. Unchanged C++ sources were hash-verified across branches and compiled once, then reused for independent branch installs. Guide-path fixes were included in final reinstall/retest where needed.

This is focused Linux installed-package validation, not a claim that complete package check, Windows/macOS, whole-package tests or biological validation passed. Hosted checks remain independently visible below.

## Final hosted CI (2026-11-01)
Exact head `407d04bde207d55fdaccf6c90ba58746b2eabf5a`: [pkgdown](https://github.com/mengxu98/scop/actions/runs/41320729681) and [R-CMD-check](https://github.com/mengxu98/scop/actions/runs/41320729670) both completed successfully. R-CMD-check includes Linux, macOS, Windows and key-Suggests jobs. Workflow success is not a zero-warning or zero-skip claim; the focused local coverage and optional native-backend limitations above still apply. This PR remains a draft and has not been merged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c839d221a731`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.