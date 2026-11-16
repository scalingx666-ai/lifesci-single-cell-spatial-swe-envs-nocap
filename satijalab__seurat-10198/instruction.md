# Issue

**Title:** Add color retrieval logic in LabelClusters for consistent cluster label coloring

## Description

Minor fix to LabelClusters logic that addresses this . Previously, when generating cluster labels, the function relied on the data passed from ggplot_build() without ensuring that point colour information was retrieved correctly. With the shift from ggplot2 v3.5.2 to ggplot2 v4+, the colour values contained in the data column are retrieved incorrectly with LabelClusters, breaking functions that use LabelClusters (DimPlot, FeaturePlot, etc.).

### Error
Previously, when LabelClusters was called within functions like DimPlot that specify label.box or custom label colours:
Ie:
```{R}
DimPlot(pbmc_small, reduction = "tsne", label.box = T, label = T)
DimPlot(pbmc_small, label.box = T, pt.size = 2, label.size = 4, label = T, cols = DiscretePalette(n = 3, palette = "polychrome"))
```

The plot would either fail to generate, generate as a blank plot, or result in the following error (or similar):
```{R}
Error in `geom.use()`:
! Problem while converting geom to grob.
ℹ Error occurred in the 2nd layer.
Caused by error:
! Unknown colour name: -5.69291337379421
```

### Fix
This fix adds a small block in LabelClusters() to retrieve the correct colour mapping from the built ggplot object (pb$data[[1]]) and append it to the label data frame. This checks for either "colour" or "color" keys and binds the appropriate column as colour, instead of looking in the first dataframe column as was done previously. If no such column exists, an NA placeholder is used to maintain compatibility.

With these changes, the following commands work on both R version 4.4.2 and 4.5.1, running either ggplot2 v3.5.2 or v4+:
```{R}
DimPlot(pbmc_small, reduction = "tsne", label.box = T, label = T)
DimPlot(pbmc_small, label.box = T, pt.size = 2, label.size = 4, label = T, cols = DiscretePalette(n = 3, palette = "polychrome"))
```
<img width="250" height="210" alt="image" src="https://github.com/user-attachments/assets/4b80a1bf-7d4d-4e9b-bbea-ce79430e7d0d" />

<img width="250" height="210" alt="image" src="https://github.com/user-attachments/assets/364ea82b-24ab-4233-bbb0-81fe3212f664" />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `244d59451c84`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.