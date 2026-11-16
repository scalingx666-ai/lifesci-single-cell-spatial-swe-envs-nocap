# Issue

**Title:** BugFix: Allow dittoHeatmap to annotate rows (genes) without annotation on columns (cells)

## Description

Fixes a bug caused by fuzzy name matching within `is.null(list$elementName)`:
- The Bug: Similarity of `annotation_colors` name within the `args` list getting built for passage to `pheatmap()`, and fuzzy name matching within `is.null()`, leads to mis-reporting of the presence of `annotation_colors` in a check for `is.null(annotation_col)`.  Specifically if `args$annotation_colors` exists, this check will report `TRUE` regardless of whether or not `args$annotation_col` truly exists.
- The Fix: This PR changes all `is.null()` calls used for this purpose to instead use `elementName %in% names(list)` syntax to ensure reporting on only exact elementName matches.

Adds:
- bug fix code
- tests (and slight cleaning)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cf888b63ba0e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.