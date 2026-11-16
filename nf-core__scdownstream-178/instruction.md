# Issue

**Title:** Implement QC anndata finalization

## Description

The new `FINALIZE_QC_ANNDATAS` in `workflows/scdownstream.nf` allows aggregating all the files in ch_obs (and other channels like ch_var etc) onto a base anndata object. This also supports CSV files (additionally to pickle files) now. Note that the CELLTYPIST process was updated: It now emits `obs` as a tuple, to also contain the `meta`. This is necessary, as otherwise we would not know which sample a certain pickle file belongs to.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `347f9e134e88`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.