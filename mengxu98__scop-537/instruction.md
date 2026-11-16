# Issue

**Title:** feat: add annotated enrichment bars with gene labels and database bands

## Description

## Summary

Add `EnrichmentPlot(plot_type = "annotated_bar")` for displaying saved over-representation results with pathway names inside horizontal bars and matching hit-gene labels underneath. Each database receives one palette color; significance controls opacity from 0.4 to 1, consistently across bars, Count dots and gene labels, following the existing GSEA bar convention.

- Rounded database bands follow the requested database order. Group panels share significance and Count scales, and named custom colors retain their database mapping.
- Reuse the existing object/result extraction, significance filtering, `id_use`, per-database top-term selection and plot-combination contracts.
- Add `show_genes`, `show_count`, `gene_width`, `row_step` and `db_gap`; compact defaults are `row_step = 0.82` and `db_gap = 0.2`. Existing plot types retain their defaults.
- Cap zero p-values before log transformation; report omitted missing p-values and reject invalid values. Labels are truncated according to character limits and bar length; actual fit remains dependent on output dimensions.

```r
EnrichmentPlot(
  object, group.by = "CellType", group_use = "Endocrine",
  db = c("GO_BP", "GO_CC", "GO_MF"),
  plot_type = "annotated_bar", topTerm = 5, palette = "Dark2"
)
```

## Validation

- Rebased onto upstream main `ad4b55530`; resolved the shared EnrichmentPlot interface/help conflicts while preserving upstream rank plots, custom result keys and score-mode handling.
- Five focused test files passed: annotated bars (63 assertions), rank plots (31), custom result keys (20), overlap (20), and annotation borders (16): 150 assertions total, with zero test failures, warnings or skips after compiling the local native library.
- `pkgload::load_all(".", quiet = TRUE, compile = FALSE)` completed after native compilation. The local testthat build-version warning is recorded separately from test results.
- Roxygen help regenerated; Rd validation and both lightweight documented rank/annotated-bar examples completed. `git diff --check` passed. styler is unavailable locally; no dependencies were installed.
- Full `rcmdcheck` with `--no-manual --as-cran --no-examples --no-tests` and `_R_CHECK_FORCE_SUGGESTS_=false` completed on the rebased implementation: 0 errors, 1 warning, 4 notes. Both `checking dependencies in R code` and `checking for unstated dependencies in examples` were OK.
- The Rd cross-reference warning exposed an upstream literal probability interval incorrectly written as a link. Fixed that source/help line in the follow-up documentation commit and regenerated/parsed the Rd successfully. The full package check was not repeated after this documentation-only correction. Unavailable local decontX/glmpca documentation references remain an environment limitation; notes cover CRAN metadata/URLs, time verification, maintainer metadata and an existing unqualified tail call.
- The initial Windows check could not link a D-drive dependency into the C-drive temporary directory. Retrying with a D-drive temporary directory completed installation and all check stages.
- Final head: `f5e6d374d`. Fresh GitHub R-CMD-check/pkgdown runs are pending; previous results do not certify this head.

No dependency or package-version changes.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b733e3ff3932`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.