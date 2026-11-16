# Issue

**Title:** Allow unnamed cols vector to be used in SpatialPlots

## Description

Fixes https://github.com/satijalab/seurat/discussions/6083

Previously, when plotting with SpatialPlot or SpatialDimPlot, users would have to pass in a named vector to the cols parameter, which is a vector of colours with each colour corresponding to an identity class (eg: 4 colours corresponding to 4 different clusters in the object). However, if this vector was not named, then the user would encounter the following error:

```
Error in `palette()`:
! Insufficient values in manual scale. 10 needed but only 0 provided.
Run `rlang::last_trace()` to see where the error occurred.
```

This is because SingleSpatialPlot specifically checks for named values in cols via ```cols <- cols[names(cols) %in% vals]```, with cols being set to NULL if no names are provided. These changes allow the user to pass a non-named vector to cols, with the colours being set to identities in order. 

Reproducible example: 
```
library(SeuratData)
brain <- LoadData("stxBrain", type = "anterior1")

DefaultAssay(brain) <- "Spatial"
brain <- SCTransform(brain, assay = "Spatial", verbose = FALSE)
brain <- RunPCA(brain, verbose = FALSE)
brain <- FindNeighbors(brain, dims = 1:20, verbose = FALSE)
brain <- FindClusters(brain, resolution = 0.3, verbose = FALSE)

#Set of custom colours
custom <- c(
  "#1f77b4",
  "#ff7f0e",
  "#2ca02c",
  "#d62728",
  "#9467bd",
  "#8c564b",
  "#e377c2",
  "#7f7f7f",
  "#bcbd22",
  "#17becf"
)

#Plotting would error without these changes
SpatialPlot(brain, cols = custom)
```

With these changes, SpatialPlot(cols = custom) now achieves the same result as using scale_fill_manual(values = custom):
<img width="587" height="489" alt="image" src="https://github.com/user-attachments/assets/00f22599-b74d-4510-9647-cfc76e7e7196" />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a18f1bdab5e5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.