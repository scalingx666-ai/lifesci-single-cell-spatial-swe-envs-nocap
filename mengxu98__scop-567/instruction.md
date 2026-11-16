# Issue

**Title:** feat: add CellStatePlot for composite cell-state summaries

## Description

## Why

Add `CellStatePlot()` to display cluster similarity, annotations, program and sample composition, marker expression and precomputed GSEA in one aligned panel. The tree describes similarity rather than time or lineage.

## What changed

- Accept loaded Seurat and Python AnnData objects, including both reticulate conversion modes. Reuse existing readers and read only the selected expression layer.
- Return a standard patchwork plot. Reuse existing grid recording and patchwork display/export mechanisms; remove the dedicated `scop_cell_state_plot` class, its methods and registrations.
- Preserve numerical summaries, annotation-map precedence, thisplot palettes and input validation.
- Use measured spacing, compact composition tracks and wrapping legends. Titles default to `NULL`; `flip = TRUE` places clusters in rows with the tree and cell-type information on the left and upright legends below.
- Match enrichment records by both cluster and pathway IDs. Share adaptive size-legend labels between layout and drawing.
- Keep dedicated helpers in one source file. Remove unused preview and snapshot assets and migrate tests to standard display, composition, conversion and rendering behavior.
- Include a complete real `pancreas_sub` example with `PrepareDB()`, `FoldChange()`, `RunGSEA()` and `CellStatePlot(..., flip = TRUE)`. Keep help concise with a one-sentence return description.

## Scope

Plot precomputed enrichment without running differential expression or enrichment inside the visualization. Reuse existing runtime dependency checks. Keep the package version unchanged.

## Verification

- An isolated installation passed 233 expectations across CellStatePlot and three related GSEA test files, with zero failures, errors or skips. Real AnnData dense/sparse inputs run under both conversion modes. One existing all-positive-score warning remains in a related GSEA test.
- Numerical data, tree, provenance, palettes, color table and dimensions match the preceding implementation.
- Default and flipped PNGs match byte-for-byte at native, short and tall sizes, six comparisons in total. Conversion through `thisplot::as_grob()` preserves the rendered PNG exactly.
- Standard automatic display, patchwork composition, vector PDF export, serialization and fresh-session printing work without the removed methods. Construction preserves graphics devices, files and RNG state.
- Existing geometry checks cover left-side annotations, upright and ascending legends, 20/50 categories, long titles and short-category headings.
- The complete real example retains all 1,000 cells and 15,998 genes, ten markers and eight GO pathways. The updated pkgdown reference and executable example built successfully with no error blocks. Eight fgsea tied-rank notices remain visible, one per group.

Validation uses the existing native library for this R-only change. The full package suite was not run.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8991cb920e1a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.