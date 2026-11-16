# Issue

**Title:** fix(RunRCTD): reject invalid counts before rounding

## Description

## Problem and change

RunRCTD silently replaced negative and non-finite spatial/reference counts with zero before preparing spacexr input. Reject these values before integer handling, with the input label in the error. Finite non-negative fractional counts retain the documented `round_counts = TRUE` rounding and `FALSE` rejection behavior.

Audit evidence: [previous preprocessing at the audited commit](https://github.com/mengxu98/scop/blob/790c367fc4008acf017b92af98a2b7c0af40fc28/R/RunRCTD.R#L456). For example, -1 or Inf previously became 0, changing the library sizes and downstream deconvolution input without an error.

## Validation

- Regression was red before the fix: all 20 invalid-value combinations were accepted (negative, NA, NaN, +/-Inf; spatial/reference; both rounding modes).
- New regression: 23 assertions pass, including fractional rounding/rejection and reordered feature/spot identifiers.
- Existing `test-rctd-cpp.R`: 25 assertions pass.
- Current cloud rerun: R 4.5.0, Seurat 5.6.0, SeuratObject 5.4.0. The 23 count-validation assertions and 25 C++ assertions passed again. This supersedes the earlier Windows validation environment.

This deliberately turns previously silently repaired invalid input into an error. Valid count matrices and the fractional compatibility option are unchanged. No spacexr fitting algorithm changes.

## Current cloud validation

The real spacexr comparison also passed all seven assertions. The input-validation change preserves valid deconvolution results; invalid-value rejection remains intentional.

## Shared Seurat compatibility follow-up

The cross-platform checks also exposed shared compatibility failures outside this spatial change. This branch now includes the common PCA/SCTransform fix:

- PCA auto fallback follows the installed Seurat implementation, including Seurat 5.6's EigenGramPCA path. Explicit backends and rank semantics are preserved; sparse-input tests assert strict upstream result/error parity.
- SCTransform handles `defer.residual.matrix` with version-aware signatures and preserves legacy `StdAssay` behavior for `do.correct.umi = FALSE` through upstream delegation.
- Neighbor tests materialize results before assertions to avoid testthat double evaluation while retaining the strict two-call check. No C++ code changes.

Cloud validation of the shared patch: PCA passed 69 assertions on Seurat 5.6 and 68 on 5.2.1; SCTransform passed 126 and 111 assertions respectively with real glmGamPoi, with no failures, errors, or skips. Seven related suites passed 333 assertions with one pre-existing optional glmpca skip. Installed lazy loading and S3 registration were checked with both Seurat versions.

## Final GitHub Actions verification

Verified on 2026-10-05 at head `665300386028339f6d70c13df6f0de7cf6558ccb`: [R-CMD-check](https://github.com/mengxu98/scop/actions/runs/37330882034) passed on Ubuntu, Windows and macOS, including the key Suggests job; [pkgdown](https://github.com/mengxu98/scop/actions/runs/37330882168) also passed. This PR remains open as a draft and has not been merged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `790c367fc400`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.