# Issue

**Title:** Add stroke.size parameter DimPlot

## Description

Hi Seurat Team,

This is PR to address #7087.  This adds the `stroke.size` parameter to `DimPlot` and consequently `SingleDimPlot`.  The parameter is set to `NULL` by default.  When this is the case the `stroke.size` is set to static value which appears to be default ggplot2 value.  I tested the plotting with this value of stroke.size vs. current DimPlot and the plots appeared identical to me.

Best,
Sam

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2a70a24f27a7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.