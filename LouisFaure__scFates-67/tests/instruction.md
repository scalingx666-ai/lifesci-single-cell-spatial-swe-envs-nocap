# Issue

**Title:** Fix batch_correct with pandas 3, copy= in diffusion/cluster, tl.cluster layer and GPU path

## Description

Bugs found while testing the GPU instructions from #66 on an NVIDIA GPU (RTX 5070, RAPIDS 26.10). None of these functions had tests, so CI never caught them.

### `pp.batch_correct` fails on CPU with pandas 3
Two pandas Series were used to index arrays:
- `X[adata.obs[batch_key] == b, :]` raised `AttributeError: 'Series' object has no attribute 'nonzero'` with scipy 1.18.
- `batch[X.indices]` raised `KeyError`, because pandas 3 treats integer keys as labels rather than positions.

Both now use numpy arrays. The GPU path already worked. CPU and GPU now agree to within 1e-5.

### `copy=True` ignored by `pp.diffusion` and `tl.cluster`
Both functions wrote into the input and returned `None`. They now work on a copy and return it.

### `tl.cluster` ignored `layer`
Since the rework in 400345a, clustering ran on `.X`, even though the default is `layer="fitted"` and the log said "Clustering features using fitted layer". The requested layer is now used.

⚠️ **Behaviour change:** results of `tl.cluster` with default arguments change for anyone whose `.X` differs from the fitted layer.

### `tl.cluster(device="gpu")` was broken
It relied on `sc.pp.neighbors(method="rapids")`. With current scanpy and cuML, that fails either way:
- **Small inputs:** scanpy's small-dataset shortcut raises `AssertionError`.
- **Larger inputs:** cuML rejects the `handle=` argument.

The GPU path now uses rapids-singlecell (`rsc.pp.pca`, `rsc.pp.neighbors`, `rsc.tl.leiden`). This replaces the cuML PCA and the hand-built cuGraph Leiden. GPU users therefore need `rapids-singlecell`; the install docs are updated in #66.

On synthetic data with 6 known modules, at 60/600/6000 features with cosine and euclidean metrics, GPU and CPU clusters are identical (ARI = 1) and recover the true modules.

### Tests
`test_preprocessing` covers `filter_cells`, `batch_correct`, and `diffusion(copy=True)`. Palantir is not a test dependency, so a small stand-in module replaces it in that test. The pipeline test now checks that `tl.cluster` uses the requested layer (replacing `.X` with noise must not change the clusters).

The new tests fail on master and pass here. CI has no GPU, so the GPU paths were checked locally only.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `42fe1151361d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.