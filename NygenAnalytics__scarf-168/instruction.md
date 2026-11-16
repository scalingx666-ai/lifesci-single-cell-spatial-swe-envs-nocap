# Issue

**Title:** Code org cleanup

## Description

## Summary
- Move Cytebase into its own package and relocate artifact lineage under `storage`, while preserving the root `scarf.ArtifactLineage` API.
- Fix Git attributes, binary handling, and source-distribution exclusions.
- Update Codecov thresholds and Read the Docs to Ubuntu 26.04 with Python 3.14.
- Add architecture and wheel checks for the retired module paths.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5e0461ebecee`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.