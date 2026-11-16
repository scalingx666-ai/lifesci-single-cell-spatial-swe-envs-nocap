# Issue

**Title:** Add alternative ggrastr-based rasterization for Dim/Feature Plots

## Description

Fixes:  

Previously, when plotting with DimPlot or FeaturePlot, users are able to set the "order" flag to True, which would ensure that points with higher values (eg: cell expression levels) are plotted atop those with lower values. However, with the adoption of geom_scattermore-based rasterization, which does not support cell order within its blending algorithm, users are unable to have both a rasterized plot with correct expression-level ordering. 

This PR addresses this issue by using ggraster::geom_point_rastr; this command rasterizes the point layer into an image when rendering the plot, and importantly maintains point order based on values. Users are able to use the geom_point_rastr render within DimPlot/FeaturePlot calls by specifying both raster = T and order = T. 

Below are plots of single-cell gene expression with these changes. The left plot was generated with ``` FeaturePlot(object, features = "rho", order = T)``` and the right plot was generated with ```FeaturePlot(object, features = "rho")```. Importantly, since the number of points within these plots exceed 100k, rasterization is used by default. With our changes, the left plot uses ggrastr::geom_point_rastr and correctly orders points by expression, while the right plot continues to use geom_scattermore and fails to order points correctly (many cells with high expression are hidden).

<img width="1042" height="484" alt="image" src="https://github.com/user-attachments/assets/2fb5c7e3-c5b4-47a0-b845-433db557747b" />

Reproducible example:

```
library(Seurat)
library(SeuratData)
library(ggrastr)
library(ggplot2)

InstallData("stxBrain")
brain <- LoadData("stxBrain", type = "anterior1")

brain <- SCTransform(brain, assay = "Spatial", verbose = FALSE)
brain <- RunPCA(brain, assay = "SCT", verbose = FALSE)

p1 <- FeaturePlot(brain, features = "Hpca", pt.size = 3, raster = T, order = T)
p2 <- FeaturePlot(brain, features = "Hpca", pt.size = 3, raster = T)
p1 + p2
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `97d59bd310f1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.