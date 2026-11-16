# Issue

**Title:** Add color_scale flexibility to layer_stat_cor_plot()

## Description

Allow 3 or more colors to be supplied to `layer_stat_cor_plot()`, this allows default to match original Purple -> Green color scale from `RColorBrewer::brewer.pal(7, "PRGn")`.

Automatically center 0 in breaks.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `26fe43ee49ae`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.