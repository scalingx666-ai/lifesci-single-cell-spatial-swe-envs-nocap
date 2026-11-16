# Issue

**Title:** Add `dittoFreqPlot()` plot

## Description

Adds (CyTOF-inspired) population frequency plotting that combines the dittoBarPlot frequency calculation machinery with dittoPlot-plotting customizations.

### Function description:
Given discrete `var` data, such as clustering or cell type-annotations, and discrete `sample.by` data, the function calculates the raw counts & percentages of cells of each sample that are associated with each value of `var` (e.g. each cell type).  Then, data is plotted grouped in the discrete access by a separately given `group.by` input and optionally subgrouped based on a `color.by` input, with faceting by `var`-data used to ensure there will be a separate plot for each e.g. cell type!  Assuming that there will be only a handful of samples in a typical dataset, I've set the default `plots` to `c("boxplot", "jitter")`.

### This PR also:
- incorporates a position-dodge fix for `plots = jitter` when color.by is used for subgrouping.
- adds a `boxplot.lineweight` control option.

### To Do:
- [x] Add a `vars.use` input for easy subsetting to just certain cell types / values of `var`
- [x] Add some scaling machinery to allow lower frequency cell types to make use of just as much plotting space as higher frequency cell types. Controlled with `max.normalize`.
- [x] Be certain of new variable names or update them: `sample.by`, `vars.use`, and `max.normalize`.
- [x] Re-finish docs
- [x] unit tests

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6284e1b8ca12`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.