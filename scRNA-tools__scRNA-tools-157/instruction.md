# Issue

**Title:** Fix for failing scheduled builds

## Description

Not sure exactly what happened but seems to be fixed by bumping **{Rcpp}** to v1.0.7.

Also update GHA caching to v2.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2d270b47a02b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.