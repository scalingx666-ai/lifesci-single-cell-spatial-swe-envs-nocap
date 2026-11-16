# Issue

**Title:** fix(prep_ref): align reference metadata with selected assay cells

## Description

prep_ref used the full object's metadata against the selected counts layer. Assay5 layers can contain only a subset of cells or a different barcode order, so metadata filtering could misalign the reference.

Align reference metadata by the selected count-matrix column names before sample/cell-type filtering, and reject missing, empty, duplicate, or unrecognized cell IDs. Full-reference behavior is retained.

Validation: the focused reference regressions passed 11 assertions, covering subset layers, shuffled counts and the full reference. The associated spatial-deconvolution and deconvolution plotting suites passed 29 and 2 assertions after updating the cloud plotting dependency to patchwork 1.3.2. These checks exercise reference preparation and plotting; they do not establish numerical equivalence of every optional deconvolution backend.

Shared test prerequisite: this branch also repairs the Seurat marker reference helper so tests preserve assay-class dispatch, with regression coverage for Assay and Assay5. The shared gate passed 106 assertions on Seurat 5.6.0 / SeuratObject 5.4.0.

Validation was performed in the cloud with R 4.5.0. Full R CMD check and final GitHub CI success are not claimed here; the broader spatial rerun and optional live-backend checks are tracked separately. This PR is intentionally a draft.

## Shared Seurat compatibility follow-up

The cross-platform checks also exposed shared compatibility failures outside this spatial change. This branch now includes the common PCA/SCTransform fix:

- PCA auto fallback follows the installed Seurat implementation, including Seurat 5.6's EigenGramPCA path. Explicit backends and rank semantics are preserved; sparse-input tests assert strict upstream result/error parity.
- SCTransform handles `defer.residual.matrix` with version-aware signatures and preserves legacy `StdAssay` behavior for `do.correct.umi = FALSE` through upstream delegation.
- Neighbor tests materialize results before assertions to avoid testthat double evaluation while retaining the strict two-call check. No C++ code changes.

Cloud validation of the shared patch: PCA passed 69 assertions on Seurat 5.6 and 68 on 5.2.1; SCTransform passed 126 and 111 assertions respectively with real glmGamPoi, with no failures, errors, or skips. Seven related suites passed 333 assertions with one pre-existing optional glmpca skip. Installed lazy loading and S3 registration were checked with both Seurat versions.

## Final GitHub Actions verification

Verified on 2026-10-05 at head `9979af7fbc04117ae4bb2bbb557e85ad701513ca`: [R-CMD-check](https://github.com/mengxu98/scop/actions/runs/37331280731) passed on Ubuntu, Windows and macOS, including the key Suggests job; [pkgdown](https://github.com/mengxu98/scop/actions/runs/37331280681) also passed. This PR remains open as a draft and has not been merged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `65373dbf2951`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.