# Issue

**Title:** SCT v2 models

## Description

- Support for fixing slope and intercept
- Support for choosing between arithmetic and geometric mean in default and offset models
- Add scale_factor option to define a custom scale factor covariate for correcting counts
- Allow plotting residual variance vs gene mean plot with respect to arithmetic mean

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ccc494bf9cd9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.