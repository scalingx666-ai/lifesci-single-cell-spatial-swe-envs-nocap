# Issue

**Title:** Realign polygon coordinates with ggplot coordinate system

## Description

# Issues

The following issues have been reported at:
- 

## Issue 1

For Spatial plots involving segmentations and an sf.data slot, there exists an inconsistency between the ggplot coordinate system and the coordinate system used by the segmentation polygons. While ggplot uses a traditional cartesian coordinate system with the origin (0,0) treated as the bottom left point of quadrant 1, segmentation coordinates are read in while treating (0,0) as their top left point. This meant that while cells could be reoriented correctly during plotting, their inherent coordinates (as used by GetTissueCoordinates) would be upside-down compared to the actual plot.

Example of what a SpatialFeaturePlot would look like if the original coordinates of cells were plotted without any transformations: 

<img width="220" height="207" alt="image" src="https://github.com/user-attachments/assets/fa1269f6-71b5-446a-8c1b-45e6b8588338" />

This lead to issues when attempting to subset Visium HD 3' datasets, as the actual locations of cells differed from where they appeared in Spatial plots:

Below figures show the actual (left) vs expected (right) cell populations when subsetting based on ggplot coordinates:
<img width="200" height="200" alt="image" src="https://github.com/user-attachments/assets/6c2a980f-6ac4-47a1-a960-75b127045f7e"/><img width="250" height="200" alt="image" src="https://github.com/user-attachments/assets/b7c974e3-8f03-43c5-a57b-94ef5dea665a" />

This fix addresses this issue by adjusting the Read10x_HD_GeoJson function in preprocessing.R to invert polygonal coordinates to match those of the ggplot coordinate system immediately as they are loaded into a Seurat object. With these changes, users will be able to subset objects by first determining a region of interest from SpatialPlots, then using GetTissueCoordinates to define cells of interest within this region.

**Reproducible Subsetting Example** (this example will produce the actual vs expected plots shown above if run on this [dataset](https://cf.10xgenomics.com/samples/spatial-exp/4.0.1/Visium_HD_3prime_Zebrafish_Head/Visium_HD_3prime_Zebrafish_Head_web_summary.html), with the actual plot resulting if you run this example before these changes):

```{R}
#Extract cellular coordinates for all cells
coords <- GetTissueCoordinates(object)

# Subset cell barcodes by x and y ranges
cells_keep <- rownames(coords)[
  coords[, "x"] >= 200 & coords[, "x"] <= 400 &
  coords[, "y"] >= 100 & coords[, "y"] <= 250
]

# Subset Seurat object to just those cells
object_subset <- subset(object, cells = cells_keep)
```

With this fix, the following should work:
- Subsetting Seurat objects containing Visium HD 3' data using GetTissueCoordinates
- Previous spatial plots involving other datasets (ie: Visium V2, Xenium) are unchanged

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `91f37305e180`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.