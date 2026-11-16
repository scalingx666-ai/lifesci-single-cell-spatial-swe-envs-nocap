# Issue

**Title:** Prepare

## Description

### Improvements to IO and feature computations
- `bento.io.prepare()`: first stab at ingesting external molecular and segmentation data 1fb026b
  - first assigns secondary seg. masks to cell in a 1-to-1 fashion
  - indexes points to cells and mapped sec. shapes
- `bento.tl.analyze_samples`: sample computation memory usage is now tractable
  - naive dask partitioning only accounted for memory footprint of `points` dataframe, but memory blowup comes from MultiIndex `groupby` operations 
  - custom partitioning ensures partitions have capped number of groupby groups
  - in the future make it a user parameter? needs more testing
- some progress bars and emojis :cake:

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f9ca5fec25f3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.