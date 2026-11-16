# Issue

**Title:** fix(spatial): align filtered predictions and honor plot controls

## Description

## Problem and behavior

Cell2location can legitimately filter zero-count observations, but its compact saved matrices were rejected by the spatial plotting ID validator. Save full-size abundance/proportion matrices with NA for filtered spots, while retaining modeled IDs in `cells`. Historical compact results are expanded only when modeled/dropped provenance explains the missing rows; malformed IDs still fail.

Long-format SpatialSpotPlot point/jitter maps now honor explicit cutoffs and quantiles and return a named list for `combine = FALSE`. Preserve their existing default full-data range. Also preserve spot IDs before assigning coordinate columns, and forward combine/layout controls for generic dominant-type maps.

Update help and the main/platform articles, and add regression coverage for filtering, serialization, historical IDs, scales, return types, and PRECAST light storage.

## Validation

- Focused regression: 48 assertions passed.
- Expanded spatial/backend regression: 3,367 assertions passed; no failures/errors; 11 existing skips. Seurat validation warnings remain.
- Rd validation and local pkgdown rebuild of the two updated articles passed.
- Real PRECAST fit on a 200-spot, two-region Visium software fixture: full/light storage from the same backend result preserved metadata, reductions, standardized values, serialization and plot data. RDS size was 3,742,619 versus 1,658,715 bytes for this fixture only. The regions are not biological replicates.
- Cell2location coverage exercises the R adapter with mocked Python output; it does not claim a new Python training run.

- Required pkgload and R CMD check completed: **0 errors, 0 warnings, 3 notes**. Both R-code dependencies and unstated example dependencies checks are OK. Notes concern CRAN incoming metadata (including existing Remotes/title/DOI formatting), current-time verification, and existing Maintainer/Authors name ordering. Check used --no-manual --as-cran --no-examples --no-tests; targeted tests ran separately. Remote incoming checks and Force-Suggests were disabled for this local check process.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `58ebec732b6d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.