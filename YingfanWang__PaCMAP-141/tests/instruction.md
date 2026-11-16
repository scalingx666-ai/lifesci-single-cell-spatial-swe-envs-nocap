# Issue

**Title:** Add support for precomputed distance matrices (resolve #12)

## Description

Allow users to pass a user-defined square (n_samples, n_samples) distance matrix to PaCMAP/LocalMAP via `distance="precomputed"`, mirroring the `metric` option available in the R wrapper and the scikit-learn convention.

When `distance="precomputed"`:
- `X` given to fit/fit_transform is treated as a distance matrix. Nearest neighbors are read directly from each row (self excluded via a masked diagonal); mid-near pairs look up matrix entries through new numba samplers (`sample_MN_pair_precomputed` and its deterministic variant); further pairs reuse the existing index-only sampler.
- Preprocessing skips normalization/PCA, `apply_pca` and `knn_backend` are ignored, and the default init falls back to 'random' ('pca' is rejected since no feature representation exists).
- `transform` raises a clear NotImplementedError, since no feature representation or index is retained for embedding new points.

Adds test/test_precomputed.py (11 tests) and documents the feature in the README, release notes, and docstrings.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d20a403473f7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.