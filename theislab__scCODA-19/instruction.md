# Issue

**Title:** Added 'level_order' for custom ordering in stacked_barplot

## Description

Hi,

just added an option to customize the order in which the different levels (x-axis) in stacked_barplot() are plotted.

Ideally, the ordering would be encoded using pd.Categorical for the `data.obs[feature_name]` column and its inherent order, but the plotting code is currently agnostic of that.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cc3e688727bc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.