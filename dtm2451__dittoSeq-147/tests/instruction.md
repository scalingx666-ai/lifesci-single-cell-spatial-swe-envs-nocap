# Issue

**Title:** Add built-in mechanism for 'dittoDotPlot()' to have a 3-color scale

## Description

This PR adds internal support for swapping `dittoDotPlot()` to use a 3-color scale.

Currently, use of a 3-color scale requires an external call to replace the fill scale, and thus loses connectivity with the function's `min`, `max`, `min.color`, `max.color`, `legend.color.breaks`, `legend.color.breaks.labels`, and `legend.color.title` input management.

Instead, this PR adds control via new inputs `mid.color` and `mid`, and allows `dittoDotPlot()` to swap as needed from passing input counterparts to `gpplot2::scale_fill_gradient()` (current, 2-color) versus `gpplot2::scale_fill_gradient2()` (new support, 3-color).
- `mid.color`: when not adjusted user gets current 2-color behavior. When given a color (string), or "rgb" or "rwb" specifically, function swaps to 3-color scale. "rgb" and "rwb" serve as a simple, single-input, provision mechanism for getting the effect of setting all of `max.color = "red", min.color = "blue", mid.color =  "gray90"` (or `"white"`).
- `mid`: `gpplot2::scale_fill_gradient2()`'s `midpoint` input equivalent, set to "make" to receive intuitive defaulting, or a number to choose a value directly.

ToDo:
- [x] develop certainty that this input mechanism is good -- the same system should be extendable to other visualizations in the future!
- [x] tests & initial documentation
- [x] finalize documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `90c3f3a3ba44`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.