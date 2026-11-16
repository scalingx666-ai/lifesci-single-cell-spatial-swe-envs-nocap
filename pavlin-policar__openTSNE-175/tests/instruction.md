# Issue

**Title:** Refactor affinity module

## Description

##### Description of changes
Adding this kind of functionality complicated things quite a bit, so a pretty major refactor was necessary to keep things manageable. Notable changes include:
- `build_knn_index` no longer computes the neighbors, but only returns the correct index. This lets us pass in already existing `KNNIndex` objects to affinities.
- All `Affinity` classes can now be called in two ways. 1) with a data matrix, as is standard, or 2) using an existing `KNNIndex` object. This is in preparation for scanpy integration, where we will have to use existing KNNGs.
- `KNNIndex` objects now have the default parameter `metric="euclidean". This just makes it easier to debug or instantiate manually.
- Add `nearest_neighbors.PrecomputedNeighbors` which allows us to wrap the standard KNNG representations.


Because there are now a whole bunch of possible ways to call this API, I added a test module which runs over the different ways to create an iris embedding. See `tests/test_different_usages.py`.

##### Includes
- [X] Code changes
- [X] Tests
- [ ] Documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `17ae1101f9f5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.