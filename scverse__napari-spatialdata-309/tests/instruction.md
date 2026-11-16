# Issue

**Title:** re-enable showing circles as points

## Description

The variable `CIRCLES_AS_POINTS` is used to determine if circles should be rendered as points (faster but viz problem when zooming in), or ellipses (precise at any zoom level but much slower).

This small PR fixes a bug that occurred when `CIRCLES_AS_POINTS` was set to `False` and also let the user change this setting by moving that variable, which before was hardcoded, to a global variable.

This PR also fixes a bug with the variable `POINT_SIZE_SCATTERPLOT_WIDGET`, which was declared but not used.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `801c50e92383`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.