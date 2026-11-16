# Issue

**Title:** Add `nucleus_shapes_key` to the writer

## Description

Previously, `explorer.write` was writing only cell boundaries, not the nucleus. This PR adds an optional `nucleus_shapes_key` to denote the name of the GeoDataFrame containing the cell nuclei.
Note that both GeoDataFrames' indices should match so that we can map every cell to a nucleus.

FYI @pakiessling and @lzyywzq, happy to get some feedback if you have some time to try it out using this branch name (`nucleus_shapes_key`)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a4267f75f33a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.