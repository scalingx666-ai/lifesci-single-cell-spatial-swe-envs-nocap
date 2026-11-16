# Issue

**Title:** Fix colouring by cells.highlight in SingleSpatialPlot

## Description

Minor fix in SingleSpatialPlot logic; previously, the variable **col.by.plot** was created from the original col.by value (variable critical for determining which data column is used for colouring cell points). However, with the shift of plotting functions to support ggplot2 v4.0.0 (), col.by.plot was introduced to safely use tidyeval syntax in ggplot aesthetics without affecting downstream string operations.

### Error

Previously, when cells.highlight is specified in plotting, the function SingleSpatialPlot creates a new "highlight" column in the data and updates col.by <- "highlight". However, since col.by.plot was already created from the original col.by value, it never reflected this change. This would result in cryptic plotting errors like:
```{R}
Error in `palette()`:
! Insufficient values in manual scale. 14 needed but only 2 provided.
```

### Fix 
Moved the cells.highlight handling block to execute before creating col.by.plot, ensuring both variables reference the same column name and synchronizing plot aesthetics and color scales.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `914c0f180bf9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.