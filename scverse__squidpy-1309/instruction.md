# Issue

**Title:** fix(gr): take the percentile threshold over edges only

## Description

## Description
`PercentilePostprocessor` now takes the percentile over off-diagonal entries only, so the diagonal zeros of `dst` no longer lower the threshold. Graphs built with `percentile` change slightly.

## How has this been tested?
New `test_percentile_ignores_diagonal` (kNN, radius, Delaunay) fails before and passes after; `test_percentile_filtering` no longer re-derives the old threshold. `tests/graph` passes.

## Closes

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d8a3195c7c4f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.