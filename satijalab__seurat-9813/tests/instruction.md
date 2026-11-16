# Issue

**Title:** Improves DimHeatmap documentation and default behavior when fast=FALSE (Issue #9810)

## Description

Clarifies documentation to specify that figure legends are currently not displayed when `fast=TRUE` but added titles with PC numbers to ggplot outputs so that both PC number and figure legends can be displayed on the same plot, plus option to move position of shared patchwork legend when `combine=TRUE` to resolve Issue

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fa638cca8a9d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.