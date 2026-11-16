# Issue

**Title:** Update plots

## Description

Most important updates:

- In **`center_scale_colour_stepsn`**
  - The default `alpha` value is now `0`
  - Update the soft pink color (#98B9FF -> #83A8F7)
- In **`bcSignatures`**
  - Correct error when the subtitle was empty ("NA" instead of nothing)
  - Correct colorbar bins
  - Avoid overlap between colorbar labels
  - Report the switch point at the bottom of the plot
  - If `blend = TRUE`, a `patchwork` of 4 plots will be returned (`ncol = 4`)
- In **`bcClusters`**: It is now possible to plot the spatial slices as a `patchwork` with a shared legend
- In **`bc4Squares`**: It is now possible to specify custom x and y cut-offs 
- In **all plots**: If the result is just one plot, return a `ggplot`/`pachwork `object rather than a list of `length = 1`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2c38ade9407a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.