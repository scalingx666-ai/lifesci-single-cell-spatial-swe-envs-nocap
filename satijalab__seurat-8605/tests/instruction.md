# Issue

**Title:** Add support for multi-modal segmentation

## Description

This adds the ability to read `segmentation_method` from the `cells.zarr.zip` for Xenium + multi-modal segmentation datasets. Zarr reading does not seem to be very straightforward with R, though, so some softdepends are needed. An example of this is shown, as well as some demonstrations on how to load other XOA outputs, in a small addition to the spatial vignette.

I also used this opportunity to clean up Xenium reading a bit, and since we will be moving from .csv.gz outputs to exclusively .parquet outputs, added support for that.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `95de9dcf9a98`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.