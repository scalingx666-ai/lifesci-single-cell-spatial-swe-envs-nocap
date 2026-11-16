# Issue

**Title:** `seq-proprocessing` restructuring; rename chapter on "feature selection & testing"

## Description

- make `seq-preprocessing` load QCed data from preceding chapter
- in `seq-preprocessing`, prettified xy-plots of marker genes (fewer genes but bigger)
- move contents from `seq-preprocessing` to corresponding `crs-` chapters; specifically
  - HVGs and DEGs to `crs-features`
  - UMAP to `crs-dimension-reduction`
  - update cross-sections references accordingly

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c0fd1c1ff3c2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.