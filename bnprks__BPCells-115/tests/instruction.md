# Issue

**Title:** [r] fix trackplot bugs with small tracks/motifs

## Description

# Description
Various small changes to coverage plots and genome peak plots to handle smaller motifs better.

- Created at least a single arrow for peaks that are not long enough for the pre-determined minimum arrow segment length.  Note, in very small peaks the arrow may go out of bounds of the peak itself, which will likely also need to be fixed in the future.
- Fixed an issue where the head_only boolean flow in `trackplot_create_arrow_segs()` did not properly assign values to the start and end position if a strand was negative.
- Fixed an issue arising from tracks smaller than 500 bp in `trackplot_coverage()`

# Tests
- Added a small test case for the head_only boolean flow in `trackplot_create_arrow_segs()`
- Added tests for small regions in `trackplot_coverage()`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b78bc8321db8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.