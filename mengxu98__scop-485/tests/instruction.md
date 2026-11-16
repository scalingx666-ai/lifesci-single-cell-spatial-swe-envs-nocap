# Issue

**Title:** fix: align deconvolution inputs on current main

## Description

## Purpose
Clean replacement for #481 on current main `215fe414`. The original branch's recent history no longer matches main, making its PR include unrelated historical commits. This fresh branch contains two focused commits and 12 files (the original 11-file fix plus one baseline CI assertion update); it preserves #483 and does not merge the divergent histories. #481 remains untouched.

## Change
- Align RCTD/CARD/SPOTlight reference labels and CARD sample metadata to selected-assay cell IDs before filtering; reject ambiguous IDs and verify input order.
- Preserve RCTD full selected-assay/layer library nUMI before analysis-gene filtering. Selected-gene counts still control zero-count filtering.
- Preserve object-wide missing-query NA results, correct dropped-type diagnostics, and include targeted regressions, optional genuine-backend smoke tests and generated docs.

All 10 non-NEWS files are byte-identical to the reviewed #481 head `7f5dda6d`. Only the 6-line NEWS entry was reapplied around current main's new entry. No additional algorithm or coordinate changes.

## Current-main CI compatibility
Merged #484 explicitly removes the thisutils SHA pin, but the metadata test still expected the old SHA. This baseline failure was reproduced on pristine main. A separate one-line test-only commit now expects the exact declared `mengxu98/thisutils` remote. The allowed package identities, `thisutils >= 0.5.2`, and all runtime checks are unchanged. The corrected metadata test passes all 4 assertions. The first fresh CI attempt stopped at this baseline assertion; the updated exact-head CI has completed successfully below.

## Verification
- Original #481 exact-head CI completed successfully on Linux, macOS and Windows, plus key-Suggests and pkgdown: [R-CMD-check](https://github.com/mengxu98/scop/actions/runs/37650473677), [pkgdown](https://github.com/mengxu98/scop/actions/runs/37650473675).
- Original local validation: 1,242 affected-suite assertions plus 35 genuine-backend smoke assertions passed. Genuine SPOTlight fits matched direct calls; genuine spacexr preprocessing validated full-depth normalization. Full RCTD fitting remains unverified because its upstream likelihood-file endpoint timed out; CARD coverage is adapter-level.
- Fresh current-base validation on `85a2a5c`: 1,233 affected-suite assertions passed with no failures/errors (3 existing warnings, 11 skips; the additional dispatch skip is intentional when SPOTlight is installed). The separate genuine-backend smoke passed all 35 assertions with zero failures/warnings/skips. R 4.5.0, Seurat 5.2.1, SeuratObject 5.1.0, SPOTlight 1.14.0 and spacexr 1.2.0. A fresh current-main DLL was reused only after comparing all 54 tracked native source files byte-for-byte.
- `git diff --check` passes. Fresh exact-head CI completed successfully on Linux, macOS and Windows, plus key-Suggests and pkgdown: [R-CMD-check](https://github.com/mengxu98/scop/actions/runs/37752946804), [pkgdown](https://github.com/mengxu98/scop/actions/runs/37752946866).
- This is a draft; no merge requested.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `215fe4141015`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.