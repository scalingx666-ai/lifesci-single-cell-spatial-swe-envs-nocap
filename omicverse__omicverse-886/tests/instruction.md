# Issue

**Title:** perf(pp): GPU chunked kNN for scdblfinder doublets

## Description

When CUDA is available, `ov.pp.qc(doublets_method='scdblfinder')` now injects omicverse's chunked-GPU exact kNN (`pp.pyg_knn_search`) into pyscdblfinder via its new `knn_fn` hook. Neighbour sets are **bit-identical** to exact sklearn (doublet class calls unchanged), while the kNN scales to 1e5–1e6-cell atlases. Guarded with `inspect` so an older pyscdblfinder without the hook still works. Requires pyscdblfinder with the knn_fn hook (omicverse/py-scDblFinder#2).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `13fc47a21410`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.