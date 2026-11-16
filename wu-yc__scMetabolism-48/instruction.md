# Issue

**Title:** Add Seurat v5 assay and visualization compatibility

## Description

Created with the assistance of Codex, GPT-5.6.
## Summary

This PR adds Seurat v5 compatibility while retaining support for older assay objects.

- Read counts using Seurat v5 layer APIs instead of accessing the removed `@counts` slot.
- Support split or merged assays containing multiple `counts.*` layers.
- Preserve the Seurat v4 `GetAssayData(slot = "counts")` fallback.
- Store metabolism scores in a valid Seurat v5 `Assay5` layer while preserving:
  `obj@assays$METABOLISM$score`
- Use `Embeddings()` and coordinate-position-based plotting so both uppercase and lowercase UMAP/t-SNE keys work.
- Align metabolism scores with reduction cell names before plotting.
- Add regression tests covering single and split v5 layers, v3-style assays, score storage, and lowercase reduction keys.





## Testing

- `devtools::test()` — 10 assertions passed.
- `R CMD check --no-examples --no-manual --no-vignettes` — tests passed.
- Tested with Seurat 5.5.1.
- The remaining package-check warnings concern existing namespace, documentation, and data-directory issues.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7208712eeb26`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.