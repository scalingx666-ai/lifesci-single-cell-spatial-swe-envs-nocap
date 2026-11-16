# Issue

**Title:** [cpp] Add dims check in `build_umap_graph_cpp`

## Description

This adds a defensive check for input dimensions to avoid messy crashes/bugs when users pass in mis-formed KNN results to `knn_to_geodesic_graph()`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `27bf508cf435`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.