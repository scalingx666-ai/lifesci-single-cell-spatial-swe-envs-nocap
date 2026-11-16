# Issue

**Title:** Replaced scran::findMarkers in findDoubletClusters() with a homebrew version.

## Description

As promised. Passes the associated tests though I haven't run `R CMD check`.

If you use `aggregateAcrossCells()`, you could get the appropriate statistics to implement a `pairwise_binom()` equivalent to `binom.test` for your other use of `findMarkers()`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b568f7d280bf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.