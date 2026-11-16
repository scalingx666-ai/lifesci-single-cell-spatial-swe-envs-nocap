# Issue

**Title:** feat: add adaptive enrichment mirror comparison plots

## Description

## Summary

Add `EnrichmentMirrorPlot()` to display two existing group-wise enrichment rankings on opposite sides of zero. This is a visualization of saved results, not a new enrichment run or a direct differential enrichment test.

- Preserve full black pathway labels even when they extend beyond bars; display matching hit-gene labels underneath, without Count dots.
- Default to blue/red group colors, support named `palcolor` mappings and shared significance opacity.
- Adapt left/right axis extents while preserving identical numeric unit lengths; optionally use symmetric extents. Label clearance is estimated from character count, not automatic device-aware font fitting.
- Provide font, size, spacing and database-band distance controls, with rounded database labels.
- Accept either the established Seurat enrichment tool key or a `RunEnrichment()` result list. Select top terms independently within each database/group, cap zero adjusted P values for display, and warn about missing adjusted P values.

```r
EnrichmentMirrorPlot(
  object, group.by = "CellType", group_use = c("GroupA", "GroupB"),
  db = c("GO_BP", "GO_CC", "GO_MF"), topTerm = 5,
  palcolor = c(GroupA = "#326A96", GroupB = "#BE4C5A"),
  symmetric_axis = FALSE, band_gap = 0.6, term_size = 3.1, gene_size = 2.3
)
```

## Validation

- Based on upstream main `8288c84cc`; independent of the still-open annotated-bar PR #537.
- Focused tests: 24 assertions passed, zero failures or test warnings. Covers selection, full labels, numeric geometry, matching colors/opacity, reversed group order, symmetric axes, missing/zero values, unbalanced databases and saved-object extraction.
- Rendered a real saved two-group GO result (30 terms) without recomputing enrichment. Private input data and generated figures are excluded from the PR.
- `pkgload::load_all(".", quiet=TRUE, compile=FALSE)` completed with fresh-worktree DLL-loading and installed testthat-version warnings recorded.
- Roxygen generated help and export; pkgdown reference index updated; `git diff --check` passed. Local styler is unavailable; no dependency installation was performed.
- Required full `rcmdcheck` (`--no-manual --as-cran --no-examples --no-tests`, `_R_CHECK_FORCE_SUGGESTS_=false`) has been started on the final source; result is pending and not counted as passed.

No package-version or dependency changes.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b733e3ff3932`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.