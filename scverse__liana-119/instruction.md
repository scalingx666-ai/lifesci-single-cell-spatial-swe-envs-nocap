# Issue

**Title:** v1.2.1

## Description

1.2.1 (11.06.2024)
-------------------------------------------------
- Added +1 to the max_neighbours to account for the spot itself in the spatial connectivities.

- Replaced Squidpy's neighbourhood graph with liana's radial basis kernel, but with a fixed number of neighbours for each spot. This does not account for edges, but differences are minimal does not require squidpy as a dependency. One can easily replace it on demand. (# )

- Fixed Python version range between 3.8 and 3.12 (Merged #112)

- Improved the Differential Expression Vignette be more explicit about the causal subnetwork search results (related to #66)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b8e7fcc77d57`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.