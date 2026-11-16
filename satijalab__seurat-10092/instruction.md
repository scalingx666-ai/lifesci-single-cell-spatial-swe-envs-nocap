# Issue

**Title:** Fix/dev

## Description

This PR proposes a batch of small fixes / changes from the Seurat development team:

- Update `PseudobulkExpression.Seurat` (). (@longmanz)
- Update `VlnPlot` to use assay passed to the function if specified (otherwise default assay) (). (@longmanz)
- Avoid `ggplot2::guides()` deprecation warnings (). (@longmanz)
- Allow plotting gene names with parentheses in `FeatureScatter` (). (@mhkowalski)
- Update `SingleRasterMap` (). (@mccormickceci)
- Make minor edit to description in PBMC3K guided tutorial vignette (). (@mccormickceci)
- Add `label.size.cutoff` parameter to `DimPlot` to allow users to label only cluster above a certain size. (@rsatija)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `38e825a64b13`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.