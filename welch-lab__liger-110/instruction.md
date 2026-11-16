# Issue

**Title:** Revised wilcoxon rank sum test - related functions

## Description

calculateWilcoxon()
-identify differentially expressed genes among different datasets within each cluster and/or among different clusters.

plotWilcoxon() 
-generate a heatmap to visualize selected top signature genes(based on Wilcoxon rank sum tests p-vals) for all clusters

Add import viridis, pheatmap

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5a8fc7b5d817`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.