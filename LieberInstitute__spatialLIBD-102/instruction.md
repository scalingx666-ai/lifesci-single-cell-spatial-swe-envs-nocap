# Issue

**Title:** Fix handling of NAs in `get_colors()`

## Description

## Background

Currently, NAs in categorical variables [are given their own color](https://github.com/LieberInstitute/spatialLIBD/blob/1836f77a635b68b32e6fe0c7ac68ad46bb1c6929/R/get_colors.R#L47). Combined with [this line](https://github.com/LieberInstitute/spatialLIBD/blob/1836f77a635b68b32e6fe0c7ac68ad46bb1c6929/R/get_colors.R#L49), this leads to the unexpected behavior that custom colors provided to `vis_clus(colors = some_colors)` are ignored for categorical variables with NAs and 12 unique non-NA values.

## Fix

After the commit in this PR, NAs are not counted as a unique color. I've checked that colors in plots now behave as expected under 12 combinations of conditions when `colors` is supplied:

- 2 or 12 clusters, including logical variables, keeping #80 in mind
- `vis_clus()` or `vis_grid_clus()`
- Including and not including NAs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1836f77a635b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.