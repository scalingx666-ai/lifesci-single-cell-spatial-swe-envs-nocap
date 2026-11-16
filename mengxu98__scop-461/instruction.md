# Issue

**Title:** fix(RunCytoSPACE): preserve cell identity and summary labels

## Description

Fix edge cases in CytoSPACE reference sampling and result summaries:

- Sample reference positions with sample.int(), so a singleton type cannot select a cell of another type through R's length-one sample() behavior.
- Preserve original cell-type labels in count/fraction tables and use collision-safe metadata suffixes.
- Avoid collisions with the total-count column and record the chosen column name and suffix mapping in stored results.
- Support empty allocations and keep zero-cell spots at zero fractions with an NA dominant type.
- Synchronize documentation and NEWS; the branch includes the current main baseline without changing its propeller fix.

Validation: 122 assertions passed in the cloud namespace/native checks, including seven new alignment tests, public workflows, empty allocations, native fraction estimation and existing CytoSPACE contracts. Actual compiled SCOP kernels were exercised. This does not establish independent numerical equivalence against the external Python CytoSPACE implementation.

Shared test prerequisite: this branch also repairs the Seurat marker reference helper so tests preserve assay-class dispatch, with regression coverage for Assay and Assay5. The shared gate passed 106 assertions on Seurat 5.6.0 / SeuratObject 5.4.0.

Validation was performed in the cloud with R 4.5.0. Full R CMD check and final GitHub CI success are not claimed here; the broader spatial rerun and optional live-backend checks are tracked separately. This PR is intentionally a draft.

## Shared Seurat compatibility follow-up

The cross-platform checks also exposed shared compatibility failures outside this spatial change. This branch now includes the common PCA/SCTransform fix:

- PCA auto fallback follows the installed Seurat implementation, including Seurat 5.6's EigenGramPCA path. Explicit backends and rank semantics are preserved; sparse-input tests assert strict upstream result/error parity.
- SCTransform handles `defer.residual.matrix` with version-aware signatures and preserves legacy `StdAssay` behavior for `do.correct.umi = FALSE` through upstream delegation.
- Neighbor tests materialize results before assertions to avoid testthat double evaluation while retaining the strict two-call check. No C++ code changes.

Cloud validation of the shared patch: PCA passed 69 assertions on Seurat 5.6 and 68 on 5.2.1; SCTransform passed 126 and 111 assertions respectively with real glmGamPoi, with no failures, errors, or skips. Seven related suites passed 333 assertions with one pre-existing optional glmpca skip. Installed lazy loading and S3 registration were checked with both Seurat versions.

## Final GitHub Actions verification

Verified on 2026-10-05 at head `44417725e7785a2e7991cbe6133d596d210aa212`: [R-CMD-check](https://github.com/mengxu98/scop/actions/runs/37331299664) passed on Ubuntu, Windows and macOS, including the key Suggests job; [pkgdown](https://github.com/mengxu98/scop/actions/runs/37331299493) also passed. This PR remains open as a draft and has not been merged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `65373dbf2951`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.