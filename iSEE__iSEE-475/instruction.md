# Issue

**Title:** Added tooltip for mouseover on DotPlots.

## Description

Note that violin plots only mouse over at their centers. Same is probably also true of hinton plots. Probably could match against the pseudo-x/y coordinates instead, in those cases.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `314a88e62f8a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.