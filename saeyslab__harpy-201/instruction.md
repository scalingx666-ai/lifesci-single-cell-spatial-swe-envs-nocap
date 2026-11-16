# Issue

**Title:** log removal of cells with no overlap with pixel cluster

## Description

- harpy.tb.cell_clustering_preprocess: log removal of instances for which there is not overlap with pixel clusters. Fix for

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `deb6bd6b749e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.