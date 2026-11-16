# Issue

**Title:** feat: add validated ATAC and multiome input interfaces

## Description

## Follow-up: active fragment resources (2026-10-14)

Latest head: `4eca5232285caa64b4800dd66930af27f624b2ac`. All configured jobs for this head completed successfully: [Linux/macOS/Windows and key-Suggests](https://github.com/mengxu98/scop/actions/runs/38545372410), plus [pkgdown](https://github.com/mengxu98/scop/actions/runs/38545372484). Success is not a zero-warning claim: Linux reported 7,465 passing assertions / 0 failures / 232 warnings / 235 skips; macOS 7,466 / 0 / 231 / 238; Windows 7,330 / 0 / 231 / 251. Their R CMD check summaries were respectively 2 warnings/2 notes, 1 warning/3 notes, and 1 warning/2 notes. All three hosted check jobs skipped four H5 tests because hdf5r was absent; the local H5 tests described below did execute. Signac >=1.17 emits a GRangesToString deprecation warning in the input fixture. Other check diagnostics include unchanged RunSingleR Rd argument documentation and, on Linux, S4Arrays/DelayedArray import replacement. Earlier validation below refers to its stated preceding heads.

`CheckATACData()` now bases fragment readiness on resources mapped to cells in the selected assay. Native Signac subsetting can retain an empty Fragment mapping when a whole capture is removed. The report keeps every resource and adds an `active` flag; inactive missing files no longer block readiness. Missing active files/indexes, incomplete coverage, and duplicate active mappings still fail readiness.

This follow-up changes only CheckATACData source/help, its input regression, and NEWS (+33/-6). Added coverage includes whole-capture subsetting, inactive missing files, active missing files, and incomplete mappings. Targeted input/multiome verification: **128 passed, 0 failed/errors/warnings/skips** (107 input +21 multiome), including actual hdf5r H5 cases, in a newly installed development package. Updated source function bodies/formals match the installed functions. Environment: R 4.4.3, Seurat 5.5.1, SeuratObject 5.4.0, Signac 1.16.0; documentation regenerated with roxygen2 8.1.0. This is targeted verification, not a new complete local R CMD check of all package tests.

---

## Summary

- Add `ReadATACData()` for sparse raw-count matrices, explicit 10x Peaks H5 files, and Matrix Market/BED/barcode inputs.
- Add `ReadMultiomeData()` for paired Gene Expression/Peaks H5 or compressed MEX input, preserving gene IDs and exact barcode alignment.
- Add non-mutating `CheckATACData()` reports for counts, genomic references, metadata, and external fragment files/mappings.
- Include generated API help, reference index entries, and deterministic testthat cases using real Seurat/Signac readers and constructors.

This is the first independent downstream ATAC batch, based on upstream main `f089f714c42a14887b8300ef485470237badd2dd`. It starts from existing peak/count data and changes no existing preprocessing or plotting implementation. FASTQ/BAM processing and peak calling are outside this batch. In particular, it does not restore the removed `cores` interfaces or SCOP's removed `SCTransform` export.

H5 input documents the native reader's minimum of two features per modality and two cells. A real one-RNA-feature H5 regression checks the explicit diagnostic when native dimensionality is dropped.

## Validation

Validated on Linux, R 4.4.3, Seurat 5.5.1, SeuratObject 5.4.0, Signac 1.16.0, and hdf5r 1.3.16:

- **24 tests / 176 assertions passed**, with zero failures, errors, warnings, or skips: ATAC input (90), paired input (21), existing GetAssayData5 slicing (7), and existing ATAC workflow regressions (58).
- All 13 added public/private installed function signatures and bodies match the final source.
- All three API help files parse successfully; the runnable `ReadATACData` public example executes successfully.
- Package source built and all 46 C++ translation units compiled and linked. `R CMD check --no-manual --no-examples --no-tests --install-args=--no-byte-compile` completed with **0 errors, 2 warnings, 6 notes**. R-code dependency checks and example dependency checks passed. Focused tests and the example above were run separately against this newly installed package.
- `git diff --check` passed. Package Version/Date and existing API implementations are unchanged.

### Check limitations

The two warnings concern GCC 16's `velocity_utils.h:357` string-operation warning and undocumented arguments in `RunSingleR.Rd`. Both files, and their relevant source, are byte-identical to the base commit. Notes cover 61 unavailable previously declared Suggests, package size, an unchanged spatial helper's unqualified `tail`, references to unavailable optional packages, existing UTF-8 data strings, and unchanged Makevars flags. All four optional dependencies added in this batch were available for the focused tests. A separate full baseline check was not rerun.

The default local install was killed during byte compilation; the successful full install/check used the standard `--no-byte-compile` option without changing package code. The `--as-cran` attempt was stopped while waiting at external incoming-feasibility checks; it is not reported as passed. Ordinary checks also reported unavailable CRAN/Bioconductor indexes in this environment.

These are current-branch input and related regression results, not a claim that the whole package suite or the historical full downstream analysis was rerun. Full normal CI has now passed on this draft's latest head; see the final result below.

## CI compatibility follow-up

The initial head exposed a real compatibility issue on R 4.6.1 / GenomeInfoDb 1.48.0: the private ATAC resolver used a namespace-local lookup, which missed public accessors re-exported from Seqinfo. The official GenomeInfoDb release NAMESPACE still exports those accessors. Commit `88053852c0d5d414eb6640ad0699bc97b0488f2d` switches that private resolver to base `getExportedValue()` without changing thisutils or adding a fallback/dependency.

A real re-exported GenomicRanges accessor reproduces the failure on the older local environment; the new regression also checks seqinfo/genome/genome replacement/seqlengths and clear missing-export errors. After reinstalling the revised R code, **185 assertions pass with zero failures, errors, warnings, or skips**, and the public example plus all 13 installed function/source comparisons pass. Native sources are unchanged; this reinstall reused their previously compiled objects. The ordinary package-check summary above belongs to the preceding head, not a new full local check of this one. New hosted CI is pending for this exact head.

The old hosted check also confirms five pre-existing SCT tests skip because glmGamPoi is not visible within the check library. Those tests are not counted as executed coverage here.

## Updated upstream integration

Upstream #496 advanced main while these checks were running. Merge commit `d674659d2f65f6e2208343350dfc496a6fd4f84e` preserves both NEWS entries and the Rcpp >= 1.0.13 requirements in Imports/LinkingTo, without rewriting branch history. Only NEWS conflicted; no functional source changed in this integration. The package was reinstalled in isolation against this merged tree, and the full focused 185 assertions, public example, and installed/source comparisons passed again. The previously compiled native objects have identical source; the new complete hosted CI run has now passed on this latest head. The PR remains a draft.

## Final CI result

Head `d674659d2f65f6e2208343350dfc496a6fd4f84e`: [R-CMD-check](https://github.com/mengxu98/scop/actions/runs/38530496961) and [pkgdown](https://github.com/mengxu98/scop/actions/runs/38530496863) both completed successfully, including Windows, macOS, Linux, and the key-Suggests job. Whole-package tests report **zero failures** on all three platforms (7,322 Windows / 7,458 macOS / 7,457 Linux passing assertions).

Coverage boundaries remain explicit: four H5 tests skip in hosted checks because hdf5r is unavailable there; those real H5 fixtures were executed in the local 185-assertion run. Five pre-existing glmGamPoi SCT tests also skip in hosted checks. Other package-wide optional/platform skips and test warnings remain. Check summaries retain the unchanged RunSingleR documentation warning, plus a SummarizedExperiment dependency-load warning on Linux; this is not a warning-free claim. This PR remains a draft for review and has not been merged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8339f62cdf83`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.