# Issue

**Title:** [r] add peak track plotting

## Description

# Description
Added function for peak track plotting using `trackplot_genome_annotations()`
Modularize code for determining vertical position for segments (`trackplot_calculate_segment_height()`), and creating continuous arrow segments (`trackplot_create_arrow_segs()`) in `trackplot_gene()`.

# Tests
Only added test case for function created for creating arrow segments `creating continuous trackplot arrows works`
I think it would be hard to make a test for `trackplot_calculate_segment_height()` because it is intrinsically random.  Certainly we set a seed but I'm not sure if future refactoring of the function would case a false positive on a regression.

# Thoughts
The direction_by arrows  don't necessarily follow  the length of the segment as I would expect.  I thought I could just do `annotation_size/(2*sin(angle))` but it looks like it is bigger than expected when playing around with plot size.  I think it could be due to the different coordinate systems of the x axis and the y axis, but I'm not 100%.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5677cf17e8a1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.