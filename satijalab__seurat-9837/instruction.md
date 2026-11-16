# Issue

**Title:** Fix ImageDimPlot & ImageFeaturePlot to allow "_" in FOV names

## Description

This PR replaces the internal separator character used by `ImageDimPlot` and `ImageFeaturePlot` with the unit separator ASCII character ("\x1F"). The functions should work properly with FOV names containing underscores ("_") from now on 👍

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d49461b44451`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.