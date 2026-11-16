# Issue

**Title:** Update combineExpression.R to allow for a custom clone definition

## Description

In the current version of combineExpression.R, the custom clone definition (specified in cloneCall) is dropped from the metadata (though clonal frequencies are still getting computed for the cloneCall). This fix prevents that.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1ae908c23946`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.