# Issue

**Title:** Issue #180

## Description

This PR depends on #204 and the `multi_table` branch of `SpatialData` and addresses all the tasks in #180 as far as they were still applicable. One difference is that it both removes `spot_diameter` and `point_diameter` as they didn't seem to have an effect. Ultimately `spot_diameter` was used in case someone clicked on an item of `AListWidget` which for some reason would add a new napari layer if the ndim of the vector was equal to 2. This has been removed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c98f28d7f3cd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.