# Issue

**Title:** feat(atac): add fixed genome-bin recounting

## Description

## Scope
Independent feature-scoped draft requested by the user: `RunGenomeTiles()` only, with verified explicit chromosome lengths and native recount into an optional new assay. No region-profile API in this branch.

Based on current main `2f44f8c52c247c5a5b42a8a2cb3a7c9800ae24cb`; does not include or alter #528/#529 or sibling new ATAC interfaces. No interactive genome browser.

## Verification
- Recovered checksum-verified source, split into an independent branch.
- `git diff --cached --check` passes; private helpers and tests are scoped independently.
- Published tree matches prepared local tree `5deaabd49668a594bbb7f3b71da2d8376b2a65f8` exactly.
- Historical combined implementation evidence: Actual indexed-fragment sparse recount, boundaries, source preservation and length validation. These prior results are NOT fresh split-branch validation.
- Fresh installed-package focused validation has now completed; see the exact-head results below. Hosted CI is reported separately and this remains a draft.

## Boundaries
Synthetic/native parity is software acceptance, not biological validation. Optional dependencies and external resource limitations remain explicit; APIs do not install packages or download reference data. No merge is requested or performed.

## Fresh exact-head validation (2026-11-01)
Head `b78d0ded870f5c08aaa0d014342643d575ec0585`, tree `5deaabd49668a594bbb7f3b71da2d8376b2a65f8`: independent package installation and installed-export isolation verified. Focused tests: **12 passing expectations, 0 failures, 0 errors, 0 skips, 1 visible upstream deprecation warnings**. R4.5.3 / Signac1.17.1 / Seurat5.5.1 / testthat3.3.2. All branch R/test/Rd source parses. Full tracked snapshot blobs match this published tree. Unchanged C++ sources were hash-verified across branches and compiled once, then reused for independent branch installs. Guide-path fixes were included in final reinstall/retest where needed.

This is focused Linux installed-package validation, not a claim that complete package check, Windows/macOS, whole-package tests or biological validation passed. Hosted checks remain independently visible below.

## Final hosted CI (2026-11-01)
Exact head `b78d0ded870f5c08aaa0d014342643d575ec0585`: [R-CMD-check](https://github.com/mengxu98/scop/actions/runs/41320758707) and [pkgdown](https://github.com/mengxu98/scop/actions/runs/41320758703) both completed successfully. R-CMD-check includes Linux, macOS, Windows and key-Suggests jobs. Workflow success is not a zero-warning or zero-skip claim; the focused local coverage and optional native-backend limitations above still apply. This PR remains a draft and has not been merged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `eaec241b700e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.