# Issue

**Title:** feat(EnrichmentPlot): optimize rank plot aesthetics, typography and non-penetrating curves

## Description

## Summary

This PR optimizes the visualization aesthetics, typography, and layout of `EnrichmentPlot(plot_type = "rank")`:

- **Highlighted Point Dark Stroke**: Added crisp `#0F172A` outline (`shape = 21`, `stroke = 0.75`) to highlighted terms, sharply defining light/pastel points against white panels.
- **Non-penetrating Z-Order**: Rendered highlighted points on top of connector lines, preventing segments from crossing into or puncturing the circle border.
- **Curved & Bolder Leader Lines**: Added gentle organic curvature (`segment.curvature = -0.10`) with slightly thicker segments (`segment.size = 0.68`, `#0F172A`).
- **Bold Top Title**: Standardized top annotation title to bold font (`face = "bold"`), matching strip headers and axis titles.
- **Zero-Void Panel Bounds**: Anchored X-axis tightly (`coord_cartesian(xlim = c(0.5, xmax + 0.6))`), completely eliminating right-side dead space.
- **Reference Gridline Control**: Standardized grid parameter as `grid_major = TRUE` (default enabled, togglable with `FALSE`), consistent with other `scop` functions.
- **Direct Parameter Reuse**: Reused existing `topTerm` directly for controlling displayed pathway counts without introducing redundant parameter aliases.
- **Default Right-Side Legend**: Defaulted legend placement to vertical right side with collected scales.

## Tests & Quality
- `styler::style_file()` applied and compliant.
- `tests/testthat/test-enrichment-rank.R`: all 37 test assertions passed (0 failures, 0 warnings, 0 skips).
- Verified end-to-end with real `pancreas_sub` dataset (`RunDEtest` + `RunEnrichment(db = "GO_BP")`).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ad4b555307dd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.