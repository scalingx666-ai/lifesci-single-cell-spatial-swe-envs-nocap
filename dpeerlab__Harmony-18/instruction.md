# Issue

**Title:** gpu additions

## Description

As discussed on issue #17, here is a pull request with gpu accelerated code added! A simple `device="gpu"` is needed when calling `harmony.core.augmented_affinity_matrix` and `harmony.plot.force_directed_layout`.

The code has been tested and needs rapids-0.17 as well as cupy>=9.0 (I haven't added these packages to the requirements, I instead mention these in the README), right now cupy 9.0 is in beta, but a stable version should be out in the coming months.

Here is what is happening when running on GPU:
* `cuml.NearestNeighbors` is used instead of `sklearn.neighbors.NearestNeighbors` and `sc.pp.neighbors`
* `cuml.LinearRegression` is used instead of `sklearn.linear_model.LinearRegression` 
* `cugraph.ForceAtlas2` is used instead of `fa2.ForceAtlas2` 
* `cuml.PCA` is used instead of `sklearn.decomposition.PCA`

As a side note, `_mnn_ka_distances` function has been slightly modified for speedups.

Here is a comparison using the included example data:

![Screenshot 2021-02-28 162055](https://user-images.githubusercontent.com/27488782/109423735-f4b3ee80-79e0-11eb-8f5a-de2aec1c8d4f.png)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `eca0771348e7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.