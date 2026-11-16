# Issue

**Title:** new version of spatialFDA

## Description

Hi, 

as mentioned before, I updated the multi-sample-colocalisation chapter to the newest version of `spatialFDA`. This brings several changes about:
- user-friendly functions `spatialInference` and `crossSpatialInference`. I hope that `spatialFDA` can be used more intuitively with these wrapper functions. 
- heatmap results across cell types. I restricted myself to two cell types for computational reasons.

The is the same as before, just with less verbose code.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `94405d9ffa42`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.