# Issue

**Title:** feat(atac): add explicit-reference bias-corrected footprints

## Description

## Scope
Independent feature-scoped draft requested by the user: `RunATACFootprint()` and `ATACFootprintPlot()` with explicit reference/bias region, native bias correction, fragment validation and cached-result receipts. The private fragment helper is independently included; no region-PR dependency.

Based on current main `2f44f8c52c247c5a5b42a8a2cb3a7c9800ae24cb`; does not include or alter #528/#529 or sibling new ATAC interfaces. No interactive genome browser.

## Verification
- Recovered checksum-verified source, split into an independent branch.
- `git diff --cached --check` passes; private helpers and tests are scoped independently.
- Published tree matches prepared local tree `5fb5fbeed1137868f117354776911b18a16b796c` exactly.
- Historical combined implementation evidence: Native corrected footprint parity on synthetic indexed fragments/reference; not biological validation. These prior results are NOT fresh split-branch validation.
- Fresh installed-package focused validation has now completed; see the exact-head results below. Hosted CI is reported separately and this remains a draft.

## Boundaries
Synthetic/native parity is software acceptance, not biological validation. Optional dependencies and external resource limitations remain explicit; APIs do not install packages or download reference data. No merge is requested or performed.

## CI packaging correction (2026-11-01)
Latest head `55a5231fed4479d44248476e5a8edde1d3f8533c`, tree `1b16fc81f49c0c463de78049927d9913e5fdcee6`: move static Markdown guides from reserved `inst/tutorials` to `inst/guides`. The original pkgdown run interpreted the reserved path as published learnr tutorials and required rsconnect. No dependency was added and no R implementation/test/help content changed. New exact-head checks are running; earlier failed CI is retained as evidence.

## Fresh exact-head validation (2026-11-01)
Head `55a5231fed4479d44248476e5a8edde1d3f8533c`, tree `1b16fc81f49c0c463de78049927d9913e5fdcee6`: independent package installation and installed-export isolation verified. Focused tests: **12 passing expectations, 0 failures, 0 errors, 0 skips, 3 visible upstream deprecation warnings**. R4.5.3 / Signac1.17.1 / Seurat5.5.1 / testthat3.3.2. All branch R/test/Rd source parses. Full tracked snapshot blobs match this published tree. Unchanged C++ sources were hash-verified across branches and compiled once, then reused for independent branch installs. Guide-path fixes were included in final reinstall/retest where needed.

This is focused Linux installed-package validation, not a claim that complete package check, Windows/macOS, whole-package tests or biological validation passed. Hosted checks remain independently visible below.

## Final hosted CI (2026-11-01)
Exact head `55a5231fed4479d44248476e5a8edde1d3f8533c`: [R-CMD-check](https://github.com/mengxu98/scop/actions/runs/41321771573) and [pkgdown](https://github.com/mengxu98/scop/actions/runs/41321771370) both completed successfully. R-CMD-check includes Linux, macOS, Windows and key-Suggests jobs. Workflow success is not a zero-warning or zero-skip claim; the focused local coverage and optional native-backend limitations above still apply. The first latest-head pkgdown attempt failed while installing unrelated reactome.db with a file-write error; one failed-job retry completed successfully without changing analysis code. This PR remains a draft and has not been merged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3ae71ccfaf7c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.