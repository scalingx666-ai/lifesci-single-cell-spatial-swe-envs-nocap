# Issue

**Title:** Added examples for read/writing, fleshed out docs.

## Description

I also tested this with:

```r
library(zellkonverter)
basilisk::setBasiliskShared(FALSE)
basilisk::setBasiliskFork(FALSE)
example(readH5AD)
sce2
```

and it does work, so everything seems in order.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b21568e173fa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.