# Issue

**Title:** Reimplement small scVelo utilities (plan steps D + E)

## Description

Replace direct scVelo imports for small plotting utilities (section D of the scVelo removal plan) and `get_moments` (section E) with private CellRank-owned reimplementations.

## New modules

- **`kernels/utils/_plot_utils.py`** — `_quiver_autoscale`, `_default_size`, `_plot_outline`
- **`kernels/utils/_moments.py`** — `_knn_moments`, `_row_normalize_connectivities`

## Changes

- **`_velocity_kernel.py`**: replace `scvelo.preprocessing.moments.get_moments` with `_knn_moments` + `_row_normalize_connectivities`
- **`_projection.py`**: replace `scvelo.tools.velocity_embedding.quiver_autoscale` with `_quiver_autoscale`; move stream/grid scVelo import behind `_check_module_importable("scvelo", extra="scvelo")`
- **`_random_walk.py`**: replace `scvelo.plotting.utils.default_size` / `plot_outline` with private helpers; replace `scv.pl.scatter` → `sc.pl.embedding`

## What this does NOT touch (later PRs)

- `scv.pl.scatter` calls in estimators/plotting (section A)
- PAGA switch to scanpy (section C)
- `pyproject.toml` dependency changes
- Test file changes

Part of: scVelo dependency reduction (#plan steps D + E)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `55c0fe635df7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.