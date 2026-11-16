# Issue

**Title:** Pseudoimage density segmentation

## Description

Add an alternative mode for segmenting the Open-ST data based on the RNA density (very simple, computes local density of total counts with a specific resolution and smoothing radius, and then applies cellpose, preferably the nuclei model).

Also, adds a preview and pseudoimage functionality that leverages napari for visualization.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `204b12ca6382`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.