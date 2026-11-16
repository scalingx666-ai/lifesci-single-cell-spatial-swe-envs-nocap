# Issue

**Title:** pairwise_aligner: rotate and flip coordinates, not images

## Description

When performing the automatic pairwise alignment, the flips & rotations prior to feature matching are applied to pseudoimage, and not to the images. This speeds up and reduces the number of layers needed in the Open-ST h5 file (does not need the uns/spatial_pairwise_aligned/... images), simplifying the workflow.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `212f78665ffa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.