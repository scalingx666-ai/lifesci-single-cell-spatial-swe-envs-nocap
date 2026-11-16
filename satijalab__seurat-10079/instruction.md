# Issue

**Title:** Fix incorrect alpha parameter being used for SpatialFeature plots

## Description

# Issues

The following issues have been reported at:
- 

## Issue 1

SingleSpatialPlot plots transparency in cells using the _alpha_ parameter. This parameter is derived in two different ways:

For DimPlots, alpha is set to be equal to pt.alpha, which is a number between 0 and 1. 

For FeaturePlots, alpha is set to be equal to alpha.by, which is set to be name of a feature (ie: alpha.by = "rho"). Then, when plotting feature plots, ggplot uses the actual values in this feature column (ie: rho expression levels), scaled between the alpha range provided (0-1) to plot the alphas. 

For objects containing sf.data, plotting was previously done only using pt.alpha. This meant that for FeaturePlots, it was not possible to set the alpha levels of cells. This fix addresses this issue by adding a check for alpha.by for plotting of objects containing sf.data; if alpha.by is found, then the plot is a FeaturePlot and ggplot will use alpha.by instead of pt.alpha to define cell transparency. 

<img width="337" height="375" alt="image" src="https://github.com/user-attachments/assets/6c3aa852-b90d-479a-ab72-50ec37cb82a5" />

With this fix, the following should work:
- SpatialDimPlot with alpha range defined (ie: c(0.2-0.6)), plot_segmentations = TRUE
- SpatialDimPlot with alpha range defined, plot_segmentations = FALSE
- SpatialFeaturePlot with alpha range defined, plot_segmentations = TRUE
- SpatialFeaturePlot with alpha range defined, plot_segmentations = FALSE

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b6c59dc139b3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.