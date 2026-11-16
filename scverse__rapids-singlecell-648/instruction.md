# Issue

**Title:** Record leiden/louvain modularity in adata.uns

## Description

As of , Scanpy records the final modularity attained by `sc.tl.leiden` in `adata.uns`. This pull-request would add the same feature to `rsc.tl.leiden` and `rsc.tl.louvain`.

Additionally, for better consistency with Scanpy, which only allows a float rather than a list of floats for the `resolution` parameter, resolution and modularity are recorded as lists in `.uns` only when a list of resolutions was passed, and as single floats otherwise.

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `42b6ea10db95`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.