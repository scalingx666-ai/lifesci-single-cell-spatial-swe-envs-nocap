# Issue

**Title:** Fix groupable

## Description

With the move to registerAppOptions, it seems the recognition of the maximum number of allowed values before a categorical variable was converted into a numeric one was not working any more for facetting, shape/size by and heatmap annotations (dot plot axes and coloring were fine). I think this should fix the issue.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `57b82e909bc5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.