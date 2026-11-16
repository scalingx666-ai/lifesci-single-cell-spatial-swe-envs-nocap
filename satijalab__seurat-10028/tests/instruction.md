# Issue

**Title:** Add support for Space Ranger cell segmentation data

## Description

# Support for Space Ranger 4.0 Spatial Datasets


<img width="767" height="412" alt="16umvspolygons" src="https://github.com/user-attachments/assets/4af0a3fd-15cc-42c4-9671-f455a3d1bfea" />

**Enhanced spatial resolution with Visium HD 3' technology.** The above spatial feature plots show `nCount_Spatial.016um` vs `nCount_Spatial.Polygons` (relative UMI counts per 16μm bin vs per cell segmentation) after pre-processing & normalization. Dataset used here is [tissue from a zebrafish head, processed with Space Ranger 4.0](https://www.10xgenomics.com/datasets/visium-hd-three-prime-zebrafish-head-fresh-frozen); visualization is from a section of the retina. Visium HD captures gene expression at subcellular resolution (~2 μm) and performs nuclei detection and expansion, enabling delineation of individual cell boundaries previously unresolvable with traditional 8/16 μm spot-based approaches.

# Introduction
This PR is built off of existing PRs, Issues, and Discussions here:
- 
- https://github.com/satijalab/seurat/discussions/9991
- 
- 
- https://github.com/satijalab/seurat/discussions/9997

In this branch, we introduce beta support for Space Ranger cell segmentation data (introduced in SR v4.0) within Seurat. Seurat currently supports the following features:

- Loading and preprocessing SR >=4.0 data with cell segmentations
- Visualization of spatial gene expression patterns
- Working with cell centroids and segmentations as distinct datatypes
- Unsupervised clustering and spatial domain identification
- Working with different resolution binnings (8μm and 16μm)
- Quality control and normalization strategies

Many thanks to @stephenwilliams22 @jsicherman from @10xgenomics for their work on the data loading functions (#9978).

# Install beta versions of Seurat and SeuratObject
Be sure to start a new session of R. This helps avoid conflicts with earlier versions which may have previously been loaded in the session.
```R
devtools::install_github("satijalab/seurat-object", ref = "spaceranger-4.0", force = TRUE)
devtools::install_github("satijalab/seurat", ref = "spaceranger-4.0", force = TRUE)
```
# Tutorial & basic workflow
A brief HTML tutorial to guide users is attached in the .zip file below:
[visiumhd3prime_commands_intro.html.zip](https://github.com/user-attachments/files/21518257/visiumhd3prime_commands_intro.html.zip)


- In `Load10X_Spatial`, users can specify `"polygons"` in the `bin.sizes` argument to load segmentations into the resulting Seurat object.
```R
v3d <- Load10X_Spatial(data.dir = data.dir,
                            slice = "slice1",
                            bin.size = c("polygons", 16))
```

- In `SpatialFeaturePlot` and `SpatialDimPlot`, users can set `plot_segmentations = TRUE` to visualize segmentations overlaid on the image.
```R
SpatialFeaturePlot(object = v3d, images = "slice1.polygons", features = "nCount_Spatial.Polygons", plot_segmentations = TRUE)

SpatialDimPlot(v3d, images = "slice1.polygons", plot_segmentations = TRUE)
```

<details>
<summary>Summary of changes to Seurat codebase</summary>

The majority of updates have been in `R/preprocessing.R` and `R.visualization.R`.

- `Load10X_Spatial` 
   - Now checks whether the user wants to load in Space Ranger 4.0 cell segmentation data from a “segmented_outputs” directory, and users can load _only_ cell segmentation data if desired
   - Reads in raw counts matrix from segmented_outputs/filtered_feature_cell_matrix.h5
   - Creates new assay “Spatial.Polygons” from counts 
   - Creates a new Visium V2 object from segmented_outputs using Read10X_Segmentations
- `Read10X_Segmentations`
   - New function that reads in a base directory of spaceranger outputs and creates a Visium V2 object 
   - Extracts scale factors from image using Read10X_ScaleFactors
   - Extracts sf object containing cell segmentation information using Read10X_HD_GeoJson
   - Returns a Visium V2 object constructed from image and segmentation data
- `Read10X_HD_GeoJson`
   - New function that reads in a .geojson file containing polygonal segmentations
   - Extracts polygon scale factors using Read10X_ScaleFactors
   - Returns an sf object containing the polygonal segmentations stored as geometries
- `Format10X_GeoJson_CellID` 
   - New function that parses segmentation cell IDs to match those of the counts layer
- `Read10X_Image`
   - Add in fallback for loading H&E stain image in case of image simlinks 
- `SpatialDimPlot`
   - Add new flag “plot_segmentations” which is FALSE by default
- `SpatialPlot`
   - Add new flag “plot_segmentations” which is FALSE by default
- `SingleSpatialPlot`
   - Add new flag “plot_segmentations” which is FALSE by default
   - Add new sf option for plotting using geom for objects containing sf geometries
   - Now has the ability to plot centroids using geom_point from an sf object
   - Now has the ability to plot polygonal segmentations using geom_sf from an sf object
   - Overlays original tissue image atop cell representations using annotation_custom 


</details>

We've aimed to maintain backwards compatibility. If users are able to test this and give feedback, including making sure that functions continue to run on existing Visium objects, that would be very helpful before the official release.

Thanks for using Seurat!

Best,
Seurat Team

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `54f8878dd9fc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.