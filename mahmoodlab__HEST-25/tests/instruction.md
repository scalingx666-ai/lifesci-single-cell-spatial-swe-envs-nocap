# Issue

**Title:** HEST-lib v1.1.0

## Description

Library release HEST v1.1.0

- Speed up import of hest lib (5X) by removing dependencies and using conditional imports
- Speed up deep learning based tissue segmentation by 10X
- Easy CellViT segmentation with cellvit-light
- Refactor tissue segmentation saving, now saving as .geojson
- Now possible to load cellvit segmentation as .parquet (10X speedup)
- Improve support for SpatialData (attaching cell segmentation)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c575887526e7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.