# Issue

**Title:** Temporarily constrain napari version

## Description

With napari version 0.5.6 there have been collisions in the shortcuts being used for both inheriting layer metadata and exporting a layer to an sdata object. This PR temporarily constrains the napari version being used.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `36fe3b96e829`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.