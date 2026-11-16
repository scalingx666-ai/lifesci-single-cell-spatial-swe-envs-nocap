# Issue

**Title:** Add stroke.size to FeaturePlot

## Description

## Summary

This PR adds support for the `stroke.size` parameter in `FeaturePlot`, consistent with its existing use in `DimPlot`. This enhancement allows finer control over point outlines, which is especially useful when visualizing datasets with a large number of cells — in such cases, points can appear cluttered or difficult to distinguish when strokes are applied.

### Example

Below is a comparison demonstrating how setting `stroke.size = 0` works on practice:

```R
fp1 <- FeaturePlot(pbmc, features = c("MS4A1", "GNLY", "CD3E", "CD14"), stroke.size = 0)
fp2 <- FeaturePlot(pbmc, features = c("MS4A1", "GNLY", "CD3E", "CD14"))

fp1 | fp2
```

<img width="1247" height="744" alt="image" src="https://github.com/user-attachments/assets/05615b49-b4b6-4a37-912b-4b5eff99b1c4" />

This PR addresses #7087 

Let me know if you want me to put the argument in different order

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e44cb2ce21af`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.