# Issue

**Title:** keep.scale for  SpatialPlot/SpatialFeaturePlot

## Description

Hi Seurat Team,

This is PR to try and address #6900.  The code and implementation is based on `FeaturePlot` implementation but obviously feel free to adjust if you have different preferences for the spatial plotting version.  It defaults to `"feature"` to scale all images to the feature max for the individual feature but also accepts `"all"` to scale all images to the global feature max of all features being plotted, or `NULL` to scale all images individually.

Best,
Sam

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `54e2fe59ad3a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.