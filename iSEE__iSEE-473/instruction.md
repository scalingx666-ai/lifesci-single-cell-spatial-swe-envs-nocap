# Issue

**Title:** Allow custom annotation to be inserted into the table.

## Description

For example:

```r
library(iSEE)
iSEEOptions$set(RowTable.select.details=function(y) {
    tagList(hr(), paste("I pity the fool who selected ", y, "!"))
})
example(iSEE, ask=FALSE)
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `654d52e84f36`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.