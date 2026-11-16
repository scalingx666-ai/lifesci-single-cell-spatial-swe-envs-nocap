# Issue

**Title:** Sc 22 aggregate

## Description

- introduction of cutom aggregate class for calculation of basic statistics using dask. Necessary due to dask_image and xrspatial implementations are slow for aggregation of many labels
- use of aggregate class in downstream `sp.tb.allocate_intensity`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e4966aaf12ff`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.