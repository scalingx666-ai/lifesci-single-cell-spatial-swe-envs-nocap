# Issue

**Title:** Add the functions for calculating the bivariate Moran index and the b…

## Description

This pull request introduces two new spatial correlation functions to the spateo package:

spatial_bv_moran_obs_genes: Calculates the bivariate global Moran’s I index for a cell's feature with specificed genes.

spatial_bv_local_moran_obs_genes: Calculates the bivariate local Moran’s I index for any two cell's features.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3722f7f5242f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.