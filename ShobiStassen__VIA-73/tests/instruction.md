# Issue

**Title:** Resolved plot_scatter bug: 'Legend' has no attribute 'legendHandles'

## Description

Updated for resolving bug with later versions of matplotlib with no `legendHandles` in `Legend` object when calling `plot_scatter()`. Resolve by generating legend based on `color_dict`.

Note: Scatters that are not present in `color_dict` will show in the plot. Also applies when plotting non-categrical labels and none of the labels are present in the `color_dict`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7ec40f98ee81`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.