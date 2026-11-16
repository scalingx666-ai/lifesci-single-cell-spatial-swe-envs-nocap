# Issue

**Title:** Drop cuml.thirdparty_adapters.check_array dependency

## Description

cuml 26.06 removed check_array from cuml.thirdparty_adapters (rapidsai/cuml#8052), breaking the rapids-prerelease CI matrix. Replaces the two check_array_cuml(init_coords, dtype=np.float32, accept_sparse=False) call sites in _draw_graph.py and _umap.py with a small local _validate_init_pos helper in tools/_utils.py — same behavior (reject sparse, coerce to cupy float32, ensure 2D), no cuml-internal dependency.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2926263a49cf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.