# Issue

**Title:** fix(SpatialSpotPlot): defer scatterpie checks for empty pie plots

## Description

## Problem and change

Empty spatial pie plots required scatterpie even when there were no polygons to draw. Move the dependency check to the nonempty rendering path so an empty result can be returned without the optional package.

The nonempty plotting path still requires scatterpie. The patch does not change the rendering algorithm or valid nonempty plot output.

## Validation

- The new regression test was red before the fix and now passes all 26 assertions.
- Focused cloud validation passed 45 tests and 258 assertions.
- A real nonempty before/after plot retained all 1,086 polygon vertices exactly.

This branch also includes the shared Seurat marker-reference dispatch helper correction and the common compatibility patch described below, so those unrelated CI failures do not obscure the spatial regression.

## Shared Seurat compatibility follow-up

The cross-platform checks also exposed shared compatibility failures outside this spatial change. This branch now includes the common PCA/SCTransform fix:

- PCA auto fallback follows the installed Seurat implementation, including Seurat 5.6's EigenGramPCA path. Explicit backends and rank semantics are preserved; sparse-input tests assert strict upstream result/error parity.
- SCTransform handles `defer.residual.matrix` with version-aware signatures and preserves legacy `StdAssay` behavior for `do.correct.umi = FALSE` through upstream delegation.
- Neighbor tests materialize results before assertions to avoid testthat double evaluation while retaining the strict two-call check. No C++ code changes.

Cloud validation of the shared patch: PCA passed 69 assertions on Seurat 5.6 and 68 on 5.2.1; SCTransform passed 126 and 111 assertions respectively with real glmGamPoi, with no failures, errors, or skips. Seven related suites passed 333 assertions with one pre-existing optional glmpca skip. Installed lazy loading and S3 registration were checked with both Seurat versions.

## Final GitHub Actions verification

Verified on 2026-10-05 at head `ccc2ad5ac652c7be7e2694b15425bf88a1d4cdbf`: [R-CMD-check](https://github.com/mengxu98/scop/actions/runs/37332043880) passed on Ubuntu, Windows and macOS, including the key Suggests job; [pkgdown](https://github.com/mengxu98/scop/actions/runs/37332044035) also passed. This PR remains open as a draft and has not been merged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `65373dbf2951`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.