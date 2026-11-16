# Issue

**Title:** Better version check for Rsubread

## Description

Current Rsubread version control leads to the following error in R 3.5.2:

```
Error in installed.packages()[grep("Rsubread", installed.packages()),  :
  subscript out of bounds
Calls: checkRsubreadVersion -> as.numeric_version -> is.numeric_version
Execution halted
```

Here `grep("Rsubread", installed.packages())` returns `c(123,1451)` and installed.packages()[c(123,1451)] leads to subscript out of bounds.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `29c776d23b07`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.