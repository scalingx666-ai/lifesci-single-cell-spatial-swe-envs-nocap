# Issue

**Title:** dittoDotPlot - respect group.by factor levels ordering

## Description

PR accomplishes exactly as the title states.  Currently, regardless of whether the `group.by` data is a factor or not, the analogous column of the data.frame created and used for plotting is of type character.  This PR adds a check of 'Is the original grouping data a factor?' then, if yes, it turns the analogous column for the plotting data.frame into a factor with the same levels.

Simply that for now, but ToDo before any merge:
- [x] Explore need for deleting unused levels
- [x] Check edge cases
- [x] function-ize this code and extend elsewhere?

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `aa7605fb2380`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.