# Issue

**Title:** PR Fixes: Fix raster warning message and pt size & PercentageFeatureSet fix

## Description

Hi Seurat Team,

This PR includes two fixes, the first is from previous PR #7938 to fix size and warnings when rasterizing points.

The second is fix for `PercentageFeatureSet` #8009 that has potential to cause incorrect values to be added to meta data (not replicated but possible) and also provides performance improvements (not running unnecessarily on non count layers).

Best,
Sam

_EDIT: fyi appears the CI fail is due to BioConductor connection issue._

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `79c2becf9baa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.