# Issue

**Title:** fix(spatial): preserve plot controls and complete shared-renderer cleanup

## Description

Explicit abundance cutoffs were overwritten by the shared matrix renderer, and Cell2location dominant maps stopped returning a list for `combine = FALSE`. Preserve explicitly requested cutoff/quantile scales and forward the dominant-map controls. Keep default matrix-wide ranges and consistent breaks for constant panels.

Long-format spatial points and jitter now reuse the standard point renderer. Consolidate spatial workflow parameter validation, stage-field updates and method-name dispatch while retaining output planning, collision checks, failure diagnostics and result probes. Runtime R sources decrease by 148 lines (58 additions, 206 deletions), excluding tests, Rd/vignettes and NEWS.

The three spatial articles now execute the SPE round-trip with `layer = 'counts'`, use merged-image auto-resolution in the PRECAST template, and render the main workflow's display-only empty-panel and real save/reload examples. Generated Rd is synchronized. Site publication remains the responsibility of the existing post-merge articles workflow.

### Validation

- Broad regression: 384 cases, 3,319 passing assertions, no failures/errors; 11 existing `skip_on_cran()` skips. Seurat validation warnings were retained.
- Against parent `893fc52c`, categorical/numeric long points and jitter (four combinations) produce equal built plotting data. A real 120-spot Visium baseline workflow produces equal metadata, stage table and native SVG results.
- Seven isolated public-data scenarios passed: Visium, BANKSY, SmoothClust, SpaNorm, local SpotSweeper, Visium HD import and Xenium import/rendering. These are small validation fixtures, not production-scale performance claims.
- All three articles built with current branch code; the corrected SPE round-trip, empty-panel example and save/reload/redraw ran. The generated figures were visually checked.
- `pkgload::load_all('.', quiet=TRUE, compile=FALSE)` passed. Final R CMD check with `--no-manual --as-cran --no-examples --no-tests` finished with **0 errors, 0 warnings, 2 notes** and R-code dependency checks OK. `_R_CHECK_FORCE_SUGGESTS_=false` and a process-local `_R_CHECK_CRAN_INCOMING_REMOTE_=false` were used; no package runtime switches were added. The notes concern existing DESCRIPTION/DOI conventions and maintainer name ordering. Rd syntax was checked separately; the modified topic has no Rd examples, while the article examples ran during rendering.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `893fc52c789e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.