# Issue

**Title:** Update on compute_driver_gene function and added 3D atlas view + 3D scatter plot

## Description

Driver genes computation updates
- Added option to use Pearson or Spearman correlation using parameter `method`
- Compute correlation with pseudo time instead of lineage likelihood
- Added pseudo time threshold to compute driver genes of intermediate state by setting pseudo time to 0 beyond the threshold

3D Atlas view
- Updated atlas embedding computation to compute 3 dimensional embedding
- Added new function `scatter3d()` in `plotting_via.py` to plot 3D scatter plots.

Minor fix to `plot_viagraph` function to plot gene expression of single gene

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `df8d76ede30a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.