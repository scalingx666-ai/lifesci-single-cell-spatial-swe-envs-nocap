# Issue

**Title:** perf(pp): GPU chunked kNN for doubletfinder pANN

## Description

`ov.pp.qc(doublets_method='doubletfinder')` now injects omicverse's chunked-GPU exact kNN into pydoubletfinder's pANN neighbour search (new `knn_fn` hook). **pANN bit-identical** to the old full-`cdist` path while avoiding its O(N²) distance matrix (OOM at ~1e5 cells). Guarded with `inspect`; needs pydoubletfinder>=0.2.0.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `119135d55098`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.