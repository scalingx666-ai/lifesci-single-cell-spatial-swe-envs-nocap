# Issue

**Title:** fix(RunBANKSY): guard independent sample coordinate fields

## Description

Add an optional sample.by guard so RunBANKSY rejects combined independent spatial samples before constructing neighborhoods. The selected assay cells must all have one non-missing, non-empty sample ID. Record the chosen metadata field in run parameters.

Clarify that BANKSY's group argument controls scaling and does not isolate spatial neighbor searches by sample. Callers should subset independent samples and run them separately. sample.by = NULL preserves existing behavior; this change does not implement multi-sample neighbor construction.

Validation: the wrapper suite passed 47 assertions, including 16 new guard/provenance assertions. Tests cover mixed or missing sample IDs, metadata-field validation and a single selected sample. Backend operations are mocked, so live BANKSY analysis is not claimed here.

Shared test prerequisite: this branch also repairs the Seurat marker reference helper so tests preserve assay-class dispatch, with regression coverage for Assay and Assay5. The shared gate passed 106 assertions on Seurat 5.6.0 / SeuratObject 5.4.0.

Validation was performed in the cloud with R 4.5.0. Full R CMD check and final GitHub CI success are not claimed here; the broader spatial rerun and optional live-backend checks are tracked separately. This PR is intentionally a draft.

## Current cloud validation

The BANKSY wrapper suite passed 47 assertions, and a live BANKSY comparison matched the corresponding upstream pipeline exactly. Cloud environment: R 4.5.0, Seurat 5.6.0, SeuratObject 5.4.0.

## Shared Seurat compatibility follow-up

The cross-platform checks also exposed shared compatibility failures outside this spatial change. This branch now includes the common PCA/SCTransform fix:

- PCA auto fallback follows the installed Seurat implementation, including Seurat 5.6's EigenGramPCA path. Explicit backends and rank semantics are preserved; sparse-input tests assert strict upstream result/error parity.
- SCTransform handles `defer.residual.matrix` with version-aware signatures and preserves legacy `StdAssay` behavior for `do.correct.umi = FALSE` through upstream delegation.
- Neighbor tests materialize results before assertions to avoid testthat double evaluation while retaining the strict two-call check. No C++ code changes.

Cloud validation of the shared patch: PCA passed 69 assertions on Seurat 5.6 and 68 on 5.2.1; SCTransform passed 126 and 111 assertions respectively with real glmGamPoi, with no failures, errors, or skips. Seven related suites passed 333 assertions with one pre-existing optional glmpca skip. Installed lazy loading and S3 registration were checked with both Seurat versions.

## Final GitHub Actions verification

Verified on 2026-10-05 at head `f22f70811ec6686fcfd1e96bffbb8d0807bd80d6`: [R-CMD-check](https://github.com/mengxu98/scop/actions/runs/37331536910) passed on Ubuntu, Windows and macOS, including the key Suggests job; [pkgdown](https://github.com/mengxu98/scop/actions/runs/37331537151) also passed. This PR remains open as a draft and has not been merged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `65373dbf2951`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.