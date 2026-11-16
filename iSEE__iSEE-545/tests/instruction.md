# Issue

**Title:** Distributed tour - ComplexHeatmapPlot elements

## Description

Notably:

- adds `.checkboxGroupInput.iSEE()`
- conditions tour step for `.selectRowRestrict` on whether the UI element is visible (it is hidden in the heat map panel)
- Bugfix for ordering of selected columns in `ComplexHeatmapPlot`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d27fb147ebc4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.