# Issue

**Title:** Add safeguard when table is None

## Description

Instantiation of `SpatialData` does not create a table, implying that the table is optional.

A SpatialData object with just (visual) elements but no annotations can still be of interest for viewing in napari-spatialdata, however it tried to load annotations without checking whether a table exists.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `02f9a76f1716`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.