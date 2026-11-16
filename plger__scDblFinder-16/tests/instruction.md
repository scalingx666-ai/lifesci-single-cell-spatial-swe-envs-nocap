# Issue

**Title:** Migrate doubletCells as computeDoubletDensity

## Description

Something worth noting here is the defensive `echo=FALSE` chunks added to some of the vignettes. These ensure that the vignette outputs are, in fact, demonstrative of the purported behavior of each function. This serves as an extra layer of testing to check that the outputs are the consistent with what we observed when we wrote the vignette.

The main drawback is that these tests are somewhat fragile as they are affected by changes anywhere in the software stack on which the function relies. But it is probably better to know about any changes earlier rather than later.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1b29b231385b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.