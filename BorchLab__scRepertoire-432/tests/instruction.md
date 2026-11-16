# Issue

**Title:** add count comparison functionality to `clonalCompare()`

## Description

To address #428, this PR adds the argument `proportion = TRUE` to `clonalCompare()`. The default behvaiour of the function is identical to previous versions, but when `prop = FALSE` it uses counts instead of frequecies.

A minor change is that when `exportTable=TRUE` the output now is sorted first if the argument was specified. Technically a breaking change but I doubt people would be affected.

The functionality works but when I test the output, I divide the exported counts by the total number of clones and try to see if it would be identical to the proportions but its not. I think I am mis-understanding the exact behaviour here @ncborcherding. Is it instead supposed to be divided only by potentially filtered counts?

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a256239d6a5e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.