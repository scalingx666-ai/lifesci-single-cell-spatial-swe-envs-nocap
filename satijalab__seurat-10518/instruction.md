# Issue

**Title:** Fix `log = T` in`VlnPlot` and preserve automatic `RidgePlot` limits

## Description

- Make `log.scale` callable in `SingleExIPlot` while preserving `VlnPlot`'s previous behavior. 
- Restore automatic limits for default `RidgePlot` calls while retaining support for explicit `y.max` and `same.y.lims`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `57ef58f818bb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.