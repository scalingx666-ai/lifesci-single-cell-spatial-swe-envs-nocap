# Issue

**Title:** Integrate scanpy for more efficient clustering and general functionality

## Description

Scanpy backend implemented

- use Scanpy Louvain clustering
- adds `tqdm` for progress bar
- validated on internal datasets
- default params run method as is in version 2.4.0
- updates umap plot by showing predicted singlets in grey, doublets in black

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d9c29e3d442e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.