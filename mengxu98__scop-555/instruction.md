# Issue

**Title:** feat(atac): add native Cicero peak coaccessibility

## Description

## Scope
Independent feature-scoped draft requested by the user: `RunATACCoaccessibility()` using the official monocle3-compatible Cicero backend. No Pearson fallback. Native NA estimates are retained and native peak-gene Links are not replaced.

Based on current main `2f44f8c52c247c5a5b42a8a2cb3a7c9800ae24cb`; does not include or alter #528/#529 or sibling new ATAC interfaces. No interactive genome browser.

## Verification
- Recovered checksum-verified source, split into an independent branch.
- `git diff --cached --check` passes; private helpers and tests are scoped independently.
- Published tree matches prepared local tree `cc88d5fc0234e11d68da244e172ccf8b46bc70f8` exactly.
- Historical combined implementation evidence: Mocked contract tests and a separately opt-in native test. Historical actual native synthetic parity used Cicero1.3.9/monocle3 1.4.26 and emitted an lme4/Matrix ABI warning; that old secondary runtime result is not fresh acceptance of this split branch. These prior results are NOT fresh split-branch validation.
- Fresh installed-package focused validation has now completed; see the exact-head results below. Hosted CI is reported separately and this remains a draft.

## Boundaries
Synthetic/native parity is software acceptance, not biological validation. Optional dependencies and external resource limitations remain explicit; APIs do not install packages or download reference data. No merge is requested or performed.

## CI packaging correction (2026-11-01)
Latest head `f835a4b596a58a0dc5a8a06da76bb3d3d05c2ab1`, tree `62712d24d5e3cbac12a424b79d4efffa65af4731`: move static Markdown guides from reserved `inst/tutorials` to `inst/guides`. The original pkgdown run interpreted the reserved path as published learnr tutorials and required rsconnect. No dependency was added and no R implementation/test/help content changed. New exact-head checks are running; earlier failed CI is retained as evidence.

## Fresh exact-head validation (2026-11-01)
Head `f835a4b596a58a0dc5a8a06da76bb3d3d05c2ab1`, tree `62712d24d5e3cbac12a424b79d4efffa65af4731`: independent package installation and installed-export isolation verified. Focused tests: **17 passing expectations, 0 failures, 0 errors, 1 skips, 1 visible upstream deprecation warnings**. R4.5.3 / Signac1.17.1 / Seurat5.5.1 / testthat3.3.2. All branch R/test/Rd source parses. Full tracked snapshot blobs match this published tree. Unchanged C++ sources were hash-verified across branches and compiled once, then reused for independent branch installs. Guide-path fixes were included in final reinstall/retest where needed.

The native Cicero opt-in test is the one skip in this fresh runtime; it is not claimed freshly executed. Contract/model dispatch tests are distinguished from the earlier separate actual native run.

This is focused Linux installed-package validation, not a claim that complete package check, Windows/macOS, whole-package tests or biological validation passed. Hosted checks remain independently visible below.

## Final hosted CI (2026-11-01)
Exact head `f835a4b596a58a0dc5a8a06da76bb3d3d05c2ab1`: [pkgdown](https://github.com/mengxu98/scop/actions/runs/41321801044) and [R-CMD-check](https://github.com/mengxu98/scop/actions/runs/41321801004) both completed successfully. R-CMD-check includes Linux, macOS, Windows and key-Suggests jobs. Workflow success is not a zero-warning or zero-skip claim; the focused local coverage and optional native-backend limitations above still apply. This PR remains a draft and has not been merged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `265891f3a983`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.