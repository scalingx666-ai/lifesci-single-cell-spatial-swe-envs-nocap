# Issue

**Title:** perf: centrality_scores as a numba BFS, drop parallelize

## Description

`centrality_scores` now runs one multi-source BFS per group in a numba kernel (`njit(parallel=True, nogil=True)`) instead of building a rustworkx graph and calling it once per category. It drops the process pool too, which was slower than serial at every scale measured.

- 2.30s -> 0.37s at 500k cells / 20 categories; 10s at 10M
- bit-exact against networkx and rustworkx on connected, disconnected and isolated-node graphs
- `backend` is deprecated the way `nhood_enrichment` deprecates it; `n_jobs` caps the numba threads
- one `_group_offsets` helper replaces the argsort grouping in `_build_shuffle_groups` and the per-library scans in `_run_spatial_neighbors`, and tolerates missing labels
- `co_occurrence` reads `.cat.codes` instead of rebuilding them in a loop (127ms -> 0.8ms at 2M cells)

Follow up:
- once fast-array-utils exposes some of these metrics as inlinable functions, we can dedup against it
- after this chain, deprecating `ImageContainer` removes the last use of `parallelize`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2dc3f07fc16b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.