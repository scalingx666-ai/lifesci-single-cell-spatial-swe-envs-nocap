# Issue

**Title:** Add layer_stat_cor_plot_complex()

## Description

Adresses #54 

Update `layer_stat_cor_plot` to use ComplexHeatmap. Prevents name cutoff, add color and annotation options as well as all other ComplexHeatmap functionality. Matches the plots we used in spatialDLPFC. 

I also suggest preserving full names in `annotate_registered_clusters()`, with the simplified names in an additional column. This prevents headaches down the road when trying to match the cluster names back up.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4359ed639f75`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.