# Issue

**Title:** Adjust dittoFreqPlot factor level retention behaviour

## Description

Removes the `retain.factor.levels` input from `dittoFreqPlot()` because the input is actually not necessary:
In practice, calculations should always run for all cell types / clusters, which can be achieved by always treating `var` as a factor.  In contrast, samples are defined to only be part of only one `group.by` and `color.by` group. Thus, calculations should only be run for the existent `group.by` and `color.by` set per sample, which can be achieved by treating these data as string/character vectors.

Addresses #93

To Do:
- [x] Unit tests
- [x] Update Documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `26310ebf75ea`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.