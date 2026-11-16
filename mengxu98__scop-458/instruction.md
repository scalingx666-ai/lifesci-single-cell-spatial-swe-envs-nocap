# Issue

**Title:** Fix SpatialNeighborhoodPlot FDR colors and sample selection

## Description

SpatialNeighborhoodPlot could retain an enriched/depleted color after the caller tightened FDR_threshold. It also plotted per-sample pair rows at the same heatmap coordinates, or stacked them in statistic bars, without making sample aggregation explicit.

This change recalculates significance using the requested threshold and adds a single-sample selector to non-spatial plots. Multiple samples now require `sample = "S1"`; remaining repeated label pairs require comparison/condition selection. No values are aggregated. Single-sample calls and observed direction labels retain their existing behavior. Spatial plots reject this new selector and direct callers to image/split.by.

Validation: regression tests failed before the change and pass afterward. The new plot regression suite and existing spatial-neighborhood, neighborhood-truthfulness, and spatial-neighborhood-backend-parity suites passed again in the cloud under R 4.5.0, Seurat 5.6.0 and SeuratObject 5.4.0. This supersedes the earlier Windows validation environment. Expected matrix coercion warnings remain. Tests check stricter thresholds, NA FDR, selected sample values and built plot layers, all three non-spatial plot types, single-sample compatibility, empty filters, and repeated comparisons.

Audit baseline: [FDR fallback](https://github.com/mengxu98/scop/blob/790c367fc4008acf017b92af98a2b7c0af40fc28/R/RunSpatialNeighborhood.R#L796), [heatmap mapping](https://github.com/mengxu98/scop/blob/790c367fc4008acf017b92af98a2b7c0af40fc28/R/RunSpatialNeighborhood.R#L829). Analysis/backend adaptation is outside this plotting change.

## Current cloud validation

The plot regression, spatial-neighborhood, neighborhood-truthfulness and backend-parity suites passed 158 assertions in the cloud, with no failures, errors or skips in those four suites.

## Shared Seurat compatibility follow-up

The cross-platform checks also exposed shared compatibility failures outside this spatial change. This branch now includes the common PCA/SCTransform fix:

- PCA auto fallback follows the installed Seurat implementation, including Seurat 5.6's EigenGramPCA path. Explicit backends and rank semantics are preserved; sparse-input tests assert strict upstream result/error parity.
- SCTransform handles `defer.residual.matrix` with version-aware signatures and preserves legacy `StdAssay` behavior for `do.correct.umi = FALSE` through upstream delegation.
- Neighbor tests materialize results before assertions to avoid testthat double evaluation while retaining the strict two-call check. No C++ code changes.

Cloud validation of the shared patch: PCA passed 69 assertions on Seurat 5.6 and 68 on 5.2.1; SCTransform passed 126 and 111 assertions respectively with real glmGamPoi, with no failures, errors, or skips. Seven related suites passed 333 assertions with one pre-existing optional glmpca skip. Installed lazy loading and S3 registration were checked with both Seurat versions.

## Final GitHub Actions verification

Verified on 2026-10-05 at head `c18ff86966c704cd3769353b85f9f42ba93a18d6`: [R-CMD-check](https://github.com/mengxu98/scop/actions/runs/37331067490) passed on Ubuntu, Windows and macOS, including the key Suggests job; [pkgdown](https://github.com/mengxu98/scop/actions/runs/37331067534) also passed. This PR remains open as a draft and has not been merged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `790c367fc400`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.