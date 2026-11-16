# Issue

**Title:** Fix spatial plots with VisiumV1 + Seurat v5.4.0

## Description

Fixes 

With the changes in Seurat v5.4.0 to load Visium (V2) data in the correct order with `imagecol` corresponding to the "y" position and `imagerow` corresponding to the "x" position, a check was added for spatial plots that would alert the user to run `UpdateSeuratObject` if their object appeared to have the old orientation of coordinates.

This is not applicable to Visium V1 images, as the `coordinates` dataframe uses the `imagecol` and `imagerow` columns directly without re-assigning to an `x` or `y` column.

To fix this error (1) and make sure spatial plots appear in the correct orientation (2), this PR proposes the following:

1) Update `SpatialPlot` to restrict the coordinate flip check to Visium V2 images only.
2) Update `GetTissueCoordinates.VisiumV1` to return the coordinate columns in the correct order (`imagecol`, `imagerow`)

```R
# Seurat object sourced from  
> v1_obj <- readRDS("~/visiumv1_275.rds")
> SpatialPlot(v1_obj, pt.size.factor = 100)
> ggsave("1.png")
# Saving 7 x 7 in image
> SpatialDimPlot(v1_obj, group.by = "orig.ident", pt.size.factor = 100)
> ggsave("2.png")
# Saving 7 x 7 in image
> SpatialFeaturePlot(v1_obj, features = "nCount_Spatial", pt.size.factor = 100)
> ggsave("3.png")
# Saving 7 x 7 in image
```
<p float="left">
  <img src="https://github.com/user-attachments/assets/52a487d2-9609-426a-a053-4e1f11368216" width="250" />
  <img src="https://github.com/user-attachments/assets/4c746ccd-78e3-4f79-9334-d8fdabeb4786" width="250" /> 
  <img src="https://github.com/user-attachments/assets/04777b5e-a64a-4077-a3f8-d21873de7e2e" width="250" />
</p>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `77d9b520b86b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.