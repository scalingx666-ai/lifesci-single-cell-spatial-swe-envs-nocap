# Issue

**Title:** fix(RunBayesSpace): honor selected metadata coordinates

## Description

When no spatial image was available, RunBayesSpace could record the requested coord.cols in provenance while constructing the backend grid from unrelated metadata coordinate columns.

Use the selected parsed pair for non-default metadata selections. Standard array-column names preserve native indices; other selected names are treated as pixel coordinates for regular-grid inference. Retain the default selection's native-array preference and existing image behavior. Update the documentation and add regressions for conflicting columns, numeric strings, custom coordinates, native indices and spot order.

Validation: all 16 wrapper tests passed, totaling 176 assertions with no failures, errors or skips. The run recorded 42 expected empty-layer warnings and optional TBB loader warnings. Backend fitting is mocked; real BayesSpace inference and full R CMD check are not established by these tests.

Shared test prerequisite: this branch also repairs the Seurat marker reference helper so tests preserve assay-class dispatch, with regression coverage for Assay and Assay5. The shared gate passed 106 assertions on Seurat 5.6.0 / SeuratObject 5.4.0.

Validation was performed in the cloud with R 4.5.0. Full R CMD check and final GitHub CI success are not claimed here; the broader spatial rerun and optional live-backend checks are tracked separately. This PR is intentionally a draft.

## Current cloud validation

Real BayesSpace validation passed 135 assertions, including the unchanged original comparison using 200 spots and 50,000 iterations. Cloud environment: R 4.5.0, Seurat 5.6.0, SeuratObject 5.4.0.

## Shared Seurat compatibility follow-up

The cross-platform checks also exposed shared compatibility failures outside this spatial change. This branch now includes the common PCA/SCTransform fix:

- PCA auto fallback follows the installed Seurat implementation, including Seurat 5.6's EigenGramPCA path. Explicit backends and rank semantics are preserved; sparse-input tests assert strict upstream result/error parity.
- SCTransform handles `defer.residual.matrix` with version-aware signatures and preserves legacy `StdAssay` behavior for `do.correct.umi = FALSE` through upstream delegation.
- Neighbor tests materialize results before assertions to avoid testthat double evaluation while retaining the strict two-call check. No C++ code changes.

Cloud validation of the shared patch: PCA passed 69 assertions on Seurat 5.6 and 68 on 5.2.1; SCTransform passed 126 and 111 assertions respectively with real glmGamPoi, with no failures, errors, or skips. Seven related suites passed 333 assertions with one pre-existing optional glmpca skip. Installed lazy loading and S3 registration were checked with both Seurat versions.

## Final GitHub Actions verification

Verified on 2026-10-05 at head `f940b5371af277e1298717071646660bd78b3d40`: [R-CMD-check](https://github.com/mengxu98/scop/actions/runs/37331516680) passed on Ubuntu, Windows and macOS, including the key Suggests job; [pkgdown](https://github.com/mengxu98/scop/actions/runs/37331516003) also passed. This PR remains open as a draft and has not been merged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `65373dbf2951`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.