# Issue

**Title:** fix h5ad

## Description

index creation would fail with `adata.obsm["spatial"]`. We settled with storing coordinates as arrays, see here for more info: https://scanpy.readthedocs.io/en/stable/api/scanpy.read_visium.html

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `42d38f6f8f8c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.