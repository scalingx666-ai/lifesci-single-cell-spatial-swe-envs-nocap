# Issue

**Title:** feat: improve BANKSY spatial analysis usability

## Description

## Summary

- Resolve `RunBANKSY(assay = NULL)` from the selected image assay, then `Spatial`, `RNA`, or `DefaultAssay`; automatically select one image and report the actual assay/image/coordinates used.
- Add `GetSpatialResult()` for cluster, parameter, and summary access, plus run receipts with domain counts and an existing `SpatialSpotPlot()` call.
- Add `sample.by` for independent BANKSY fits, named sample-to-image maps, sample-prefixed labels, and per-sample result retrieval.

## Migration

`assay = NULL` may now select a different assay; set `assay` explicitly to reproduce an older analysis. Use `sample.by` for independent fits; `group` remains an algorithm scaling parameter, and domains are not aligned across samples. The layer default is unchanged; a missing layer reports available layers without normalizing or switching automatically.

## Validation

- `pkgload::load_all('.', quiet=TRUE, compile=FALSE)` passed.
- BANKSY, spatial receipt, raw-default, input-contract, coordinate-contract v3, and spatial-plot-contract tests passed after rebasing to current `upstream/main`.
- `tools::checkRd()` and Rd example parsing passed for the changed topics; `pkgdown::build_reference_index()` passed.
- Windows `R CMD check --no-manual --as-cran --no-examples --no-tests` completed with package installation and example dependency checks OK. It reports two unrelated existing warnings (`thisplot::NetworkPlot` / `thisutils::fit_trends` exports and undocumented arguments in `RunSingleR.Rd`) and four notes; the CRAN URL checks also encountered TLS handshake failures. A local untracked `CODE_REVIEW.md` caused a top-level-file note during this check and is not part of the PR.

## Follow-up fixes and validation (2026-10-07)

Initial fix revision: `c654f0e4351536ca00fa40cc3b95e4603834647c`; synchronized with main `24f4698` without rewriting the existing branch history. These initial results are retained below; the current-head integration results follow in the final section.

- Retain a lightweight result index when `store_results = FALSE`: exact analyzed cell/sample membership and the custom cluster-column/tool mapping. Samples such as `S1` and `S1_A` are never inferred from cluster-label prefixes. Detailed backend objects and parameters remain omitted.
- Clear old cluster labels for cells excluded by a rerun, including zero-count spots. Regression tests cover stale default results, custom columns/tools, both storage modes, overlapping sample names, metadata edits, and failed-sample atomicity.
- Metadata-only legacy objects without a reliable sample index still support whole-object cluster retrieval; sample-specific retrieval now requests a rerun rather than guessing membership.
- Cloud Linux / R 4.5.0: all 14 BANKSY wrapper/regression cases passed (677 assertions, 0 skips), including the five wrapper groups previously skipped for missing SpatialExperiment.
- Real Banksy 1.6.0: a 96-spot, two-sample test with overlapping sample names and shared coordinates matched separate standalone fits in both storage modes (17 assertions, 0 skips). The existing 150-spot comparison with the original Banksy pipeline also passed (3 assertions, 0 skips). Domains remain independent and are not aligned across samples.
- Full native SCOP compilation and installation succeeded. Changed Rd topics passed `tools::checkRd()` and example parsing. Examples check backend availability without installing it.
- Local integration of current main, this revision, and #478 passed 80 related cases / 1,138 assertions with no failures, errors, or skips, using SeuratObject 5.1.0. The 109 warnings were existing Seurat object-validation/key warnings. The source tarball built successfully and excluded the root contribution guide.
- CI now installs Banksy, SpatialExperiment, and BiocNeighbors, requires nonempty zero-skip BANKSY/real-backend and spatial-alias results, and keeps the original assertions. [Exact-revision R-CMD-check](https://github.com/mengxu98/scop/actions/runs/37604366427) passed on Ubuntu, macOS, Windows, and the key-Suggests job. The [dedicated backend job](https://github.com/mengxu98/scop/actions/runs/37604366427/job/112736162970) also passed with R 4.6.1, Banksy 1.8.1, SpatialExperiment 1.22.0, BiocNeighbors 2.6.0, and SeuratObject 5.4.0.
- Full check results: Ubuntu 6,944 PASS / 0 FAIL, macOS 6,937 / 0, Windows 6,856 / 0. Other optional tests remain skipped in the hard-dependency jobs (224 / 227 / 239 respectively); the targeted BANKSY and alias suites are verified separately with zero skips. Existing package warnings/notes remain, including the root contribution-guide note addressed separately by #478.
- [pkgdown](https://github.com/mengxu98/scop/actions/runs/37604366473) passed and actually built the reference index and new GetSpatialResult page. The PR workflow did not rebuild the existing RunBANKSY page or the full site, and deployment was skipped.

Known pre-existing compatibility limitation: the broader receipt suite reproduced two failures on unchanged main with SeuratObject 5.0.2 because its Assay5 VariableFeatures getter returns incorrect indices. The same main test passed 30/30 with official SeuratObject 5.1.0. Version 5.0.2 remains within the declared dependency range; this is not claimed to be an unsupported configuration or fixed by this BANKSY PR.

## Final integration validation (2026-10-07)

Current head: `23e490b36ae9cfe626057ab796988c49442c830a`, incorporating main `309240ac6298842d8622055edf0adb47d89a40df`, including #478 and the upstream #479 GSVA fix. The only merge conflict was the adjacent `NEWS.md` additions; both BANKSY migration notes and GSVA release notes were retained. No additional BANKSY runtime changes were needed.

- The exact published tree matched the locally validated tree. The 80 spatial/BANKSY integration cases passed again (1,138 assertions, 0 failures/errors/skips), along with both new upstream GSVA regression cases (50 assertions, 0 failures/errors/skips). Existing Seurat object-validation/key warnings remain.
- [Current-head R-CMD-check](https://github.com/mengxu98/scop/actions/runs/37616500792) passed all four jobs. Ubuntu: 6,994 PASS / 0 FAIL; macOS: 6,987 / 0; Windows: 6,906 / 0. The hard-dependency checks retained 224 / 227 / 239 optional-test skips respectively; this is not a zero-skip full-suite claim.
- The [key-Suggests job](https://github.com/mengxu98/scop/actions/runs/37616500792/job/112775991334) passed gene-set scoring, BANKSY wrapper regressions, real multisample backend parity, original Banksy pipeline parity, and spatial object-alias contracts. BANKSY and alias checks require nonempty results with zero skips.
- [Current-head pkgdown](https://github.com/mengxu98/scop/actions/runs/37616500790) passed. The R package checks report top-level files OK after #478; pre-existing documentation/environment warnings and Makevars notes remain. Runnable examples are excluded by the package-check command.

The previously disclosed SeuratObject 5.0.2 compatibility limitation remains unchanged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `309240ac6298`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.