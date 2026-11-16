# Issue

**Title:** Add raster.dpi param for geom_scattermore (updated branch)

## Description

Hi Seurat Team,

Just quick PR supporting what I think seems like good feature request in #5388. This adds relevant new parameter `raster.dpi` to relevant plots that use `geom_scattermore`. I have also added appropriate documentation and a warning check to make sure that supplied values for `raster.dpi` are valid. Pretty sure I caught all the spots (`SingleCorPlot` and `SingleDimPlot` and their downstream functions).

Similar to `raster` I set parameter to NULL in the base plotting functions and set default value in downstream functions (to value that is equivalent to current scattermore defaults). Alternatively could change it so that parameter is NULL in downstream functions and add code so that if left NULL it will default to `c(512, 512)` if you think that's better on user end.

Thanks again!
Sam

*Note: This is resubmission of previous PR #5391.  Just decided to make it easy and fetch changes upstream and remake the PR rather than resolving conflicts.*

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8da35ba8dc2d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.