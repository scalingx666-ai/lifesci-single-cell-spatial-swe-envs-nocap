# Issue

**Title:** Fix DR baselines

## Description

This PR fixes various [problems](https://deploy-preview-121--openproblems-sca.netlify.app/benchmarks/dimensionality_reduction/) with the dimensionality reduction baselines.

* density_preservation was giving a correlation of 0.5 when comparing the true data to itself
* spectral distances should be optimized by spectral embeddings
* spectral distances should weight the eigenvectors by their eigenvalues
* Removed some unnecessary baselines
* Added a diffusion maps method (incidental, through spectral distance fix) and a zebrafish dataset (as all existing datasets were rather simple)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c50ae881efe2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.