# Issue

**Title:** Allow 'dittoDotPlot()' 'vars' to be grouped into categories

## Description

PR allows for grouping of `vars` (e.g. by celltype) in a `dittoDotPlot()` by giving the `vars` input a list rather than simple vector.

Also adds input `vars.dir` for controlling the axis where `vars`-data will be shown. 

ToDo:
- [x] Finalize docs descriptions, including edge-case interactions with `split.by`
- [x] Decide whether / how to update include `theme(panel.*)` & `split.adjust` adjustments to beautify.
  - Scoped and added with control via new inputs `categories.split.adjust` and `categories.theme.adjust`.
    - Either can be turned off by setting these to FALSE.
    - Both are constrained, when possible, to the axes where `vars.dir` axis.
- [x] unit test for base functionality
- [x] unit tests for new variables

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4fc5e6e918d2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.