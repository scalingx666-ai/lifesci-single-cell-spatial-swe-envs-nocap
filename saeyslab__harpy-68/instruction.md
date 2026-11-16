# Issue

**Title:** Sc 33 performance plot shapes on translated

## Description

- faster plotting of a shapes layer in `sp.pl.plot_shapes` when there is a transformation defined on the shapes layer
- add `sp.sh.vectorize `to API + add fallback to vectorize using skimage instead of rasterio, related to

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d10ed68d4451`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.