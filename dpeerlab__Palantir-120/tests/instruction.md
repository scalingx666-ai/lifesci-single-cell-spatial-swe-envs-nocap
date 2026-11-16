# Issue

**Title:** Refactor run_diffusion_maps

## Description

## Refactor `run_diffusion_maps` to Modularize Kernel Computation and Eigen Decomposition

This commit separates the functionality of `run_diffusion_maps` into two
distinct sub-functions: `compute_kernel` handles the adaptive anisotropic
kernel calculation, while `diffusion_maps_from_kernel` performs the eigen
decomposition for the diffusion maps.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8fba608e215b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.