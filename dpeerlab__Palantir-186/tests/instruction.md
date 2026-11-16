# Issue

**Title:** Faster, leaner pseudotime on large data

## Description

Makes `_compute_pseudotime` faster and lighter on large data. Pseudotime and `W` are bit-identical to `master`'s, on the data below and on the tutorial's marrow sample. 471k cells, 30-NN graph, 1,195 waypoints, 8 cores:

| step | `master` | this PR | how |
| --- | --- | --- | --- |
| connectivity check | 66 s | 0.7 s | `_connect_graph` uses scipy's `csgraph.dijkstra` instead of networkx. Same repair loop and same graph, except where two cells tie exactly for farthest reachable |
| shortest paths from the waypoints | 623 s | 91 s | waypoints split over `n_jobs` processes; scipy's `dijkstra` holds the GIL, so threads don't help |
| refinement | 31 s | 27 s | chunks of at most 10,000 cells. Exact: each cell depends only on its own column, and equal chunk sizes keep numpy's summation order |
| total | 725 s | 123 s | |
| peak memory, workers included | 26.8 GiB | 10.5 GiB | the refinement's temporaries are per chunk; `W` isn't copied into its DataFrame |

- On small data the processes cost nothing (#176): on the 4,142-cell marrow sample, 2.0 s serial and 1.4–1.8 s on 8 processes. Where `_get_joblib_backend` picks threads (Python ≥ 3.12, joblib < 1.5), this step stays serial.
- networkx is no longer imported; I can drop the dependency here if you'd like.
- Tests in `test_core_equivalence.py`: the equivalence test also runs with `n_jobs=2` and small chunks; a new test checks that chunks and processes are bit-identical (it fails if a one-cell chunk is left over); another compares `_connect_graph` with the networkx original on a disconnected graph.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f819d5156c8f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.