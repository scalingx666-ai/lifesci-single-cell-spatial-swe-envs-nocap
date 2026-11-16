# Issue

**Title:** optimize umap func

## Description

Our umap function will calculate umap from scratch and then construct UMAP object if return_mapper is True. After optimization, the function will construct UMAP object directly and extract the necessary information from it when return_mapper is True.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fba189a0accc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.