# Issue

**Title:** feat(atac): add assay-specific motif sequence logos

## Description

## Scope
Independent feature-scoped draft requested by the user: `ATACMotifPlot()` only, using explicit motif IDs and the selected assay's PWM list. Adds optional ggseqlogo, focused tests, help and tutorial. Based on current main `2f44f8c52c247c5a5b42a8a2cb3a7c9800ae24cb`; does not include or alter #528/#529 or other new ATAC interfaces. No interactive genome browser.

## Verification
- Source restored from the checksum-verified prior delivery and split into an independent branch.
- `git diff --cached --check` passes; no sibling feature/helper dependencies. Published tree matches the prepared local tree `d523f45ade719882d4c633fcc3f07b1c59d09469` exactly.
- Historical combined implementation had native motif-logo parity tests. Those prior combined results are NOT represented as fresh tests of this split branch.
- Fresh installed-package focused validation has now completed; see the exact-head results below. Hosted CI is reported separately and this remains a draft.

## Limits
Motif similarity is not proof of TF binding. Native dependency warnings remain visible. No automatic dependency installation or reference download occurs within the API.

## CI packaging correction (2026-11-01)
Latest head `dbf567f8bb8ac5936f6c70455861a7ef570bff72`, tree `1db547ffca09574248d34a935b9e89a4c1564b40`: move static Markdown guides from reserved `inst/tutorials` to `inst/guides`. The original pkgdown run interpreted the reserved path as published learnr tutorials and required rsconnect. No dependency was added and no R implementation/test/help content changed. New exact-head checks are running; earlier failed CI is retained as evidence.

## Fresh exact-head validation (2026-11-01)
Head `dbf567f8bb8ac5936f6c70455861a7ef570bff72`, tree `1db547ffca09574248d34a935b9e89a4c1564b40`: independent package installation and installed-export isolation verified. Focused tests: **3 passing expectations, 0 failures, 0 errors, 0 skips, 3 visible upstream deprecation warnings**. R4.5.3 / Signac1.17.1 / Seurat5.5.1 / testthat3.3.2. All branch R/test/Rd source parses. Full tracked snapshot blobs match this published tree. Unchanged C++ sources were hash-verified across branches and compiled once, then reused for independent branch installs. Guide-path fixes were included in final reinstall/retest where needed.

This is focused Linux installed-package validation, not a claim that complete package check, Windows/macOS, whole-package tests or biological validation passed. Hosted checks remain independently visible below.

## Final hosted CI (2026-11-01)
Exact head `dbf567f8bb8ac5936f6c70455861a7ef570bff72`: [R-CMD-check](https://github.com/mengxu98/scop/actions/runs/41321670465) and [pkgdown](https://github.com/mengxu98/scop/actions/runs/41321670457) both completed successfully. R-CMD-check includes Linux, macOS, Windows and key-Suggests jobs. Workflow success is not a zero-warning or zero-skip claim; the focused local coverage and optional native-backend limitations above still apply. This PR remains a draft and has not been merged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2f44f8c52c24`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.