# Issue

**Title:** fix #412

## Description

use `adata.uns.get('bin_size', 1)`
in stereo_to_anndata

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e1fe543a9b9b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.