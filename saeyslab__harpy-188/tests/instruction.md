# Issue

**Title:** Fix MACSima IO naming/docs and preserve point metadata through Dask ops

## Description

Fix for 
Make ROI ID inclusion in MACSima channel names optional (include_roi_id_in_channel_name)

Update MACSima docs/examples to reflect recursive .tif discovery and ROI-per-path expectation.

Preserve SpatialData point transform metadata across Dask persist(), sample(), and query() to avoid validation errors.

Changes
-  optional ROI in channel names; docs/examples updated for recursive glob usage.
- : retain .attrs after persist() to keep transform.
- restore .attrs after sample() / query().

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a76379d5b505`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.