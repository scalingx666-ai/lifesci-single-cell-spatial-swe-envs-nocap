# Issue

**Title:** Edge-case bugfix to ensure non-NULL SE names for empty SEs.

## Description

Fixes the following:

```r
library(iSEEu)
example(LogFCLogFCPlot)
iSEE(se[,0], list(LogFCLogFCPlot()))
## Something about assigning NULL to ColorBySampleName.
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e25b8f6474d8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.