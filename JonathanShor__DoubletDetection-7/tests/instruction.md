# Issue

**Title:** create_synthetic_data improvements

## Description

TODOs completed:
-  TODO: pick celltype to mix with chance proportional to cellcounts

TODOs progressed:
- TODO: Revise to remove doublet noise (to at least some degree)
Introduced parameter shrink, should be a float in [0.0, 1.0]. That
percent of cells in each cluster (rounded down) will be pruned, in
order by most distant (eucl dist) from cluster centroid.

utils.py minor changes:
- dataAcquisition: added read_rows parameter to read only first X rows
of  file. Defaults to entire file.
- Bug fixes in testModel.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `66b8c585add0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.