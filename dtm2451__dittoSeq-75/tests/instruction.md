# Issue

**Title:** Add histogram shape option to `dittoPlot()`/`dittoRidgePlot()`

## Description

Re #71, adds shape control to the dittoPlots with `plot = "ridgeplot"` via 3 inputs:

- `ridgeplot.shape`: switch between "smooth", default, or "hist"
- `ridgeplot.bins` & `ridgeplot.binwidth`: control the number of bins or bin size, respectively, for the histogram shape.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2e1f17418ad0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.