# Issue

**Title:** Add aspect ratio specification to spatial plots when crop = FALSE

## Description

## Issue
In Seurat  >= `v5.4.0`, setting `crop = F` in spatial plots produces a distorted image if the features/clusters highlighted do not appear in a region similar to the original aspect ratio of the tissue image.

## Current visualization
Here, `brain` is the object retrieved after processing in the [spatial vignette](https://satijalab.org/seurat/articles/spatial_vignette).

When `crop = F` (not the default), the image appears distorted:

```R
brain_subset <- subset(brain, idents = c(3, 4, 7))
SpatialDimPlot(brain_subset, label = T, label.size = 3, crop = F)
```
<img width="300" alt="image" src="https://github.com/user-attachments/assets/b3971231-f6d9-4ea8-906c-8008dabf713b" />
<br/>
<br/>

Note that this isn't an issue / isn't applicable when `crop = T` (default). This is because in this case, the plot should only show the features/clusters local to their position on the tissue image, and thus doesn't require a set aspect ratio.

```R
SpatialDimPlot(brain_subset, label = T, label.size = 3, crop = T)
```
<img width="300" alt="image" src="https://github.com/user-attachments/assets/391e8581-6b00-44a2-8f33-923f777b3ab7" />


## Fixed visualization

When returning the plot in `SingleSpatialPlot`, if `crop = F` the aspect ratio of the image is set inside a theme layer `theme(aspect.ratio = _ )`. Since this is a conditional check, there is no change to `crop = T` with the proposed fix.

```R
brain_subset <- subset(brain, idents = c(3, 4, 7))
SpatialDimPlot(brain_subset, label = T, label.size = 3, crop = F)
```
<img width="300" alt="image" src="https://github.com/user-attachments/assets/a87d3318-0202-4673-b15d-4721fbf2c2ab" />

### Side by side comparison
<img width="300" alt="image" src="https://github.com/user-attachments/assets/b3971231-f6d9-4ea8-906c-8008dabf713b" /> <img width="300" alt="image" src="https://github.com/user-attachments/assets/a87d3318-0202-4673-b15d-4721fbf2c2ab" />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ab112196bd5a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.