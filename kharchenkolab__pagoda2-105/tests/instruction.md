# Issue

**Title:** Remove unused/outdated functions

## Description

As recommend by @VPetukhov, I took a stab at removing some outdated functions. 

* I don't see `fast.pca()` used in `helpers.R`
* The only thing used in `dendrogram.R` is `my.heatmap2`
* I left everything in `cell.sorting.R` untouched, as these functions are documented and exported. 
* I didn't see anything in `p1app4p2.R` used, so I removed it. 

Naturally, I could be making mistakes, so let's triple check this.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `27d4e278143d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.