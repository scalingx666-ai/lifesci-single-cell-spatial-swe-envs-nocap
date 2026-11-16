# Issue

**Title:** Fix interactive functionality of spatial plotting functions

## Description

# Changes

Main:
- `ISpatialDimPlot`
  - (context: called from `SpatialDimPlot(..., interactive = T)`)
  - Set `xvar` and `yvar` properly in call to `shiny::nearPoints`
  - Flip y coordinate when setting/displaying coordinate info for hover/clicked points (harmonize w/ image space)
- `LinkedDimPlot`
  - Specify `xvar` and `yvar` in call to `shiny::brushedPoints` for the dim plot
- `LinkedFeaturePlot`
  - Separate data for spatial and dim plot similar to setup in `LinkedDimPlot`

Supporting:
- `SpatialPlot`
  - Make sure that alpha is set to a contrasting range (`c(0.1,1)`) in interactive mode (if default, which is `c(1,1)`) so that clusters are properly highlighted upon click
  - Provide more informative messages for errors arising from mismatches between specified arguments and data that actually exists in the object (i.e. when the specified image and default assay don't match, or when the default assay set doesn't have data corresponding to the default ident - the second case can occur when, for example, `Spatial.Polygons` is the default assay but we attempt to plot with `Spatial.008um` which only has `counts` and has not been processed)
- `SingleDimPlot`
  - Handle the `alpha.by` parameter properly
    - (This is not actually available for users to specify in `DimPlot`, but is used in `LinkedDimPlot` to highlight clusters on the dim plot when a cell is clicked)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `24495e3e6e90`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.