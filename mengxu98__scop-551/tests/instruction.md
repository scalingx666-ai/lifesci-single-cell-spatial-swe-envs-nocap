# Issue

**Title:** feat(atac): add mapped fragment-length QC plots

## Description

## Scope
Independent feature-scoped draft requested by the user: `ATACFragmentPlot()` with explicit regions, selected assay cells and per-file barcode mappings. Regional fragment histograms are not whole-library estimates.

Based on current main `2f44f8c52c247c5a5b42a8a2cb3a7c9800ae24cb`; does not include or alter #528/#529 or sibling new ATAC interfaces. No interactive genome browser.

## Verification
- Recovered checksum-verified source, split into an independent branch.
- `git diff --cached --check` passes; private helpers and tests are scoped independently.
- Published tree matches prepared local tree `fbac1e8414296fbd43ac5538477f6f95003db80a` exactly.
- Historical combined implementation evidence: Native histogram parity and input nonmutation. These prior results are NOT fresh split-branch validation.
- Fresh installed-package focused validation has now completed; see the exact-head results below. Hosted CI is reported separately and this remains a draft.

## Boundaries
Synthetic/native parity is software acceptance, not biological validation. Optional dependencies and external resource limitations remain explicit; APIs do not install packages or download reference data. No merge is requested or performed.

## CI packaging correction (2026-11-01)
Latest head `97ef3966f3465b7a14c8864bb136247f72d20597`, tree `e4a9105e8f8c687451bb9b46fb67188c6f2a2981`: move static Markdown guides from reserved `inst/tutorials` to `inst/guides`. The original pkgdown run interpreted the reserved path as published learnr tutorials and required rsconnect. No dependency was added and no R implementation/test/help content changed. New exact-head checks are running; earlier failed CI is retained as evidence.

## Fresh exact-head validation (2026-11-01)
Head `97ef3966f3465b7a14c8864bb136247f72d20597`, tree `e4a9105e8f8c687451bb9b46fb67188c6f2a2981`: independent package installation and installed-export isolation verified. Focused tests: **16 passing expectations, 0 failures, 0 errors, 0 skips, 1 visible upstream deprecation warnings**. R4.5.3 / Signac1.17.1 / Seurat5.5.1 / testthat3.3.2. All branch R/test/Rd source parses. Full tracked snapshot blobs match this published tree. Unchanged C++ sources were hash-verified across branches and compiled once, then reused for independent branch installs. Guide-path fixes were included in final reinstall/retest where needed.

This is focused Linux installed-package validation, not a claim that complete package check, Windows/macOS, whole-package tests or biological validation passed. Hosted checks remain independently visible below.

## Final hosted CI (2026-11-01)
Exact head `97ef3966f3465b7a14c8864bb136247f72d20597`: [R-CMD-check](https://github.com/mengxu98/scop/actions/runs/41321684340) and [pkgdown](https://github.com/mengxu98/scop/actions/runs/41321684276) both completed successfully. R-CMD-check includes Linux, macOS, Windows and key-Suggests jobs. Workflow success is not a zero-warning or zero-skip claim; the focused local coverage and optional native-backend limitations above still apply. This PR remains a draft and has not been merged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2f44f8c52c24`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.