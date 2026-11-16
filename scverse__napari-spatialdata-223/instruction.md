# Issue

**Title:** adjust to join_spatialelement

## Description

In spatialdata we adjusted the function `join_sdata_spatialelement_table`. The function is now called `join_spatialelement_table` and works both inside and outside the `SpatialData` object. I adjusted the code here to reflect this.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bcde6e28117b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.