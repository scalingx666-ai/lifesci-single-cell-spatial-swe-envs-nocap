# Issue

**Title:** Clear errors in linearity_deviation for invalid paths and empty groups

## Description

Addresses #37 and #35. Both crashes in `tl.linearity_deviation` came from inputs the function didn't check.

### #37: `'NoneType' object has no attribute 't'`
`getpath` only walks segments in their `from → to` direction. It returns `None` when `end_milestone` isn't downstream of `start_milestone`: the two are swapped relative to the root, or they're sibling tips. Reproduced on the test dataset (root 43) with `start_milestone="88", end_milestone="43"` and `"18" → "88"`. It now raises:

> No path found from start_milestone '88' to end_milestone '43' following the direction of the tree (root: '43'). end_milestone must be downstream of start_milestone: try swapping them, or re-root the tree with scf.tl.root and scf.tl.pseudotime.

### #35: `zero-size array to reduction operation maximum`
If no cells fall below the low percentile or above the high one, the mean profile `A` or `B` is all NaN. statsmodels' formula API then drops every row, and `np.max` fails on the empty design matrix. This can happen when many cells share the same pseudotime at either end of the path, because the comparisons are strict (`<` / `>`). Reproduced with `percentiles=[0, 80]` and `[20, 100]`. It now raises:

> No cells found in: putative progenitors (t < 0.0824), among the 444 cells on the path 43->88 with percentiles=[0, 80]. This can happen when many cells share the same pseudotime value (e.g. at the start or end of the path); try adjusting the percentiles.

(The pandas `drop_duplicates` part of #35 was already fixed: `bifurcation_tools.py` now uses `keep=False`.)

### Also
- An unknown `start_milestone` / `end_milestone` now raises a `ValueError` that lists the available milestones.
- Results on valid inputs are unchanged (the `43->88` values match master).
- Added `pytest.raises` checks for all three cases in `test_w_plots.py`.

### CI fix: pin `umap-learn<0.6` (pixi env only)
umap-learn 0.6.0 came out on 2026-11-10. Its numba kernels require a C-contiguous `knn_dists`, but scanpy's brute-force kNN path, used for small inputs, can return a non-contiguous array. That breaks `scf.tl.cluster` (cosine metric on the transposed gene matrix) with a `TypingError`, and CI was failing on that call independently of this change. The pin applies only to the pixi environment; the package's own dependencies are unchanged. Upstream fix: scverse/scanpy#4480, merged but not yet in a release (latest is 1.12.5). Once scanpy ships it, the pin can be replaced by a scanpy lower bound.

The Build and Test workflow now also runs when `pyproject.toml` changes. Before, a dependency-only commit triggered no tests.

### Testing
`pixi run test-cov` passes locally and in CI. Codecov: all modified lines are covered, and project coverage went from 80.73% to 80.81%.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8d8c0e629d71`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.