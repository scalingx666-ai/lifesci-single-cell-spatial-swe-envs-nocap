# Issue

**Title:** Enforce sensible defaults for the dynamic selection setting.

## Description

This fixes a nasty bug:

- Set `iSEEOptions$set(dynamic.selections.multiple=TRUE)` 
- Make a multiple row selection on some panel X, e.g., a `RowDataPlot`.
- Any column-based panels (say, panel Y) will auto-set their row multiple selections to panel X. 

Normally this isn't a big issue, but if X takes a column selection, then you now have an unnecessary circularity whenever you try to make a selection on Y. This is most problematic if X is a `DifferentialStatisticsTable`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5864c04ed3cf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.