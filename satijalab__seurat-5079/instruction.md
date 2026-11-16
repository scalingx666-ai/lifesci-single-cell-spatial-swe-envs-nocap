# Issue

**Title:** Skip groups with fewer than default min.cells.group

## Description

# Problem
The current behavior of FindConservedMarkers is the following:
If a group has exactly 0 cells in an Identity, it skips with a warning and no error. If a group has between 1 and min.cells.group (default=3) cells in an Identity, it errors due to ValidateCellGroups. I think a better behavior would be for it to also skip with a warning in this case.

Related issue: #1971

# Implementation
I checked for the number of cells in ident.1 before continuing and created a warning for that case.

I have implemented this behavior in the best way I could, but I am not sure if there is a better solution. Thank you.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `826d5474bb90`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.