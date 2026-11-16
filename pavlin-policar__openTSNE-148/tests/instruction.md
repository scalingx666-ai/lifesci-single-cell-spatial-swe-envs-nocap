# Issue

**Title:** Add hnswlib as k nearest neighbour index

## Description

##### Issue
The kNN algorithms available in openTSNE are not as fast and/or memory efficient as HNSW (https://arxiv.org/abs/1603.09320).
Furthermore, Annoy, BallTree, and pynndescent are not made for high-dimensional data; For example, Annoy even throws an error above 1000 dimensions.

##### Description of changes
This pull request ...
* adds hnswlib as a dependency
* adds option to choose 'hnswlib' to `build_knn_index` for `Affinities`
* implements additional `KNNIndex` class to interface with hnswlib

##### Includes
- [X] Code changes
- [x] Tests
- [x] Documentation

If you like the idea of having HNSW as an alternative, I'll add tests and some documentation.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ceb105e8e8b4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.