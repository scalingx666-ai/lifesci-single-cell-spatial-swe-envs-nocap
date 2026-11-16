# Issue

**Title:** update GSVA function with new name

## Description

As of 2 weeks ago (in ), GSVA renamed their function `compute.gene.density` as `compute.gene.cdf`. I've updated the corresponding code in `densityEnrichment`. 

Thanks for this package – super useful with some great visualizations!

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `192e127971e1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.