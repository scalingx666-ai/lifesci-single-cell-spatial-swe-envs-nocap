# Issue

**Title:** Add rasterization options for scatterplot functions.

## Description

This still needs tests and has a quirk or two I can't figure out. Namely, the size of the gray cells when using `cells.use` with `dittoDimPlot` does not seem to take into account the `size` argument, and I don't know why.

Regardless, this adds simple rasterization parameters to `dittoScatterPlot` and `dittoDimPlot` (and by extension, the multiplotters), thereby allowing PDF output to be much easier to load/edit in third party programs (e.g. Illustrator). This is particularly useful with many cells and multiple figure panels.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `367000ce4f73`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.