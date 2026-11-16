# Issue

**Title:** Fixed error computing differential expression results using scanpy in…

## Description

…  `cirro prepare_data` with older h5ad files

Raise error in `cirro prepare_data` when specified group not found in dataset

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `661e7a0cfa43`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.