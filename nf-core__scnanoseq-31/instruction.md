# Issue

**Title:** Closing issue #30 by exporting home in process

## Description

This PR closes issue #30 by simplifying usage of the pipeline without the need set `export NXF_SINGULARITY_HOME_MOUNT=true` for users using Singularity, and without having to set a warning in the documentation.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ddb0c28ffd7a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.