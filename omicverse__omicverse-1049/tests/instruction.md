# Issue

**Title:** pp.ambient: soupx resolves the cluster column like decontx

## Description

## Problem

`_run_soupx` set `has_clusters = cluster_key is not None and cluster_key in adata.obs`. With no `cluster_key`, it skipped `pysoupx.auto_est_cont` and silently set rho = 0.1. The documented call `ov.pp.ambient.remove_ambient(adata, method='soupx', raw=raw_adata)` passes no `cluster_key`, so on a clustered AnnData with `obs['leiden']` it used a fixed 0.1 instead of SoupX's automatic estimate. `_run_decontx` already finds the column through `_resolve_clusters`.

## Change (`omicverse/pp/ambient/_ambient.py`)

- The candidate lookup moved out of `_resolve_clusters` into `_find_cluster_key`, which returns the column or `None` and never raises. DecontX and scCDC behave as before.
- When `cluster_key` is None, `_run_soupx` picks the first existing column out of `clusters`, `leiden`, `louvain`, `cell_type`, `celltype`, and passes it to `SoupChannel.from_anndata` so clusters are set on the channel. `auto_est_cont` then runs.
- If no column exists and `contamination_fraction` is not set, the 0.1 fallback stays. It now emits a `UserWarning` that names the value and says to pass `cluster_key=` or `contamination_fraction=`. The warning points at the user's `remove_ambient` / `estimate_contamination` call. If an explicit `cluster_key` is not an `obs` column, the same warning names that key. Before this change it fell back silently.
- `uns['ambient']['cluster_key']` (and `estimate_contamination(...).attrs`) now records which column was used.
- The `cluster_key` docstring in `remove_ambient` describes the auto-lookup and the fallback.

Behaviour change to note: a clustered AnnData now runs `auto_est_cont`. If that column has no usable markers (for example a single cluster), SoupX's own error now surfaces. Before, such data silently got 0.1. This matches what already happens with an explicit `cluster_key`.

## Tests (`tests/pp/ambient/test_soupx_cluster_key.py`)

- **Real pysoupx** (`pytest.importorskip`): a synthetic raw + filtered channel with 8 clusters, marker blocks and a true rho of 0.2.
  - With `obs['leiden']` and no `cluster_key`, `remove_ambient` and `estimate_contamination` return `auto_estimated=True` and `cluster_key='leiden'`, emit no fallback warning, and the estimate (about 0.16) is closer to 0.2 than the 0.1 fallback is.
  - Without any cluster column, they warn and use 0.1 for every cell, with `auto_estimated=False`.
- **Faked backend** (always runs; CI installs `.[tests,mcp]`, not `omicverse[ambient]`, so the tests above are skipped there):
  - Each candidate column reaches `from_anndata` and `auto_est_cont`.
  - An explicit key wins over the candidates.
  - No clusters: warning, 0.1, `adjust_counts(clusters=False)`.
  - A missing explicit key is named in the warning.
  - An explicit `contamination_fraction` gives no warning.

Local runs:
- Against unfixed master: 11/12 new tests fail. The only pass is the explicit-rho case, which never depended on the bug.
- With the fix and pysoupx 0.1.1: `tests/pp/ambient/` 31 passed.
- Without pysoupx: 9 passed, 3 skipped.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0fd38b79d790`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.