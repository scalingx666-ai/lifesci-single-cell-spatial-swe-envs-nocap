# Issue

**Title:** Parallelize spatial neighbors

## Description

## Description

This PR addresses two performance leverages in sptial_neighbors:
 * extract per-library sub-matrices upfront and once (most important)
 * enable per-library parallelism with joblib (relatively high per-worker overhead, only worthwhile with many samples)

The first step brings down the runtime by ~50% in my real-world dataset.
Parallelism doesn't add a ton, but still slightly improves the wall time. It really depends on the dataset how much it adds, therefore I left the default at `n_jobs=1`. 

When working with spatialdata, there's an additional bottleneck in `_prepare_spatial_neighbors_input` that I'll follow up on separately. 

## How has this been tested?

- unit tests pass
- manually on a real-world dataset

## Closes

no related issue

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `da789d0b10fb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.