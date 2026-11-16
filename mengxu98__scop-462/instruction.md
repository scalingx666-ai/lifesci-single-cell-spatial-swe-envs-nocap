# Issue

**Title:** fix(RunCSIDE): align finite covariates with retained spot IDs

## Description

Single-mode C-SIDE preprocessing filtered the barcode vector for finite explanatory values but still forwarded the unfiltered explanatory vector. This could leave backend covariates inconsistent with the retained spots.

Subset explanatory.variable using the same finite-value mask as barcodes before dispatch. Document the exclusion of missing/non-finite values and add regressions for shuffled named covariates and missing condition metadata.

Validation: the RunCSIDE wrapper suite passed 95 assertions, including 26 assertions in the two new alignment tests. The existing summary-truthfulness test passed 2 assertions with an expected matrix-coercion warning. These use backend mocks and do not claim a completed live spacexr C-SIDE fit; the cloud loader also reported optional TBB/DLL warnings.

Shared test prerequisite: this branch also repairs the Seurat marker reference helper so tests preserve assay-class dispatch, with regression coverage for Assay and Assay5. The shared gate passed 106 assertions on Seurat 5.6.0 / SeuratObject 5.4.0.

Validation was performed in the cloud with R 4.5.0. Full R CMD check and final GitHub CI success are not claimed here; the broader spatial rerun and optional live-backend checks are tracked separately. This PR is intentionally a draft.

## Shared Seurat compatibility follow-up

The cross-platform checks also exposed shared compatibility failures outside this spatial change. This branch now includes the common PCA/SCTransform fix:

- PCA auto fallback follows the installed Seurat implementation, including Seurat 5.6's EigenGramPCA path. Explicit backends and rank semantics are preserved; sparse-input tests assert strict upstream result/error parity.
- SCTransform handles `defer.residual.matrix` with version-aware signatures and preserves legacy `StdAssay` behavior for `do.correct.umi = FALSE` through upstream delegation.
- Neighbor tests materialize results before assertions to avoid testthat double evaluation while retaining the strict two-call check. No C++ code changes.

Cloud validation of the shared patch: PCA passed 69 assertions on Seurat 5.6 and 68 on 5.2.1; SCTransform passed 126 and 111 assertions respectively with real glmGamPoi, with no failures, errors, or skips. Seven related suites passed 333 assertions with one pre-existing optional glmpca skip. Installed lazy loading and S3 registration were checked with both Seurat versions.

## Final GitHub Actions verification

Verified on 2026-10-05 at head `bfc3c1009ae3a8596e72d325a7d90e8526ff6ace`: [R-CMD-check](https://github.com/mengxu98/scop/actions/runs/37331485560) passed on Ubuntu, Windows and macOS, including the key Suggests job; [pkgdown](https://github.com/mengxu98/scop/actions/runs/37331485381) also passed. This PR remains open as a draft and has not been merged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `65373dbf2951`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.