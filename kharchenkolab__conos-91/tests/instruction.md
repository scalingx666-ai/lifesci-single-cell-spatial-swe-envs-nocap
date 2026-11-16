# Issue

**Title:** Add parameter `raster.dpi` in `con$plotEmbedding()`

## Description

Add parameter `raster.dpi` in `con$plotEmbedding()` to replace `raster.height` and `raster.width`, given these parameters are defunct with rewrite of `ggrastr` (v0.2.0)[https://github.com/VPetukhov/ggrastr/releases/tag/v0.2.0]

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c2d0cb2309ff`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.