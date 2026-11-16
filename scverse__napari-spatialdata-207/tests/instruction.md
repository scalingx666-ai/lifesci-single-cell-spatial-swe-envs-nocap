# Issue

**Title:** Issue #192

## Description

This PR fixes the issue that the visibility of coordinate systems is not properly updated when having multiple spatialdata objects with different coordinate systems. See issue #192 for the reproducible example. This PR works with the reproducible example.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ce5c19809ddb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.