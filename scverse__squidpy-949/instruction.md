# Issue

**Title:** Added function to download Visium as SpatialData

## Description

The `squidpy.datasets` function were downloading AnnDatas or ImageContainers. For a lot of work, I'd love to have an easy SpatialData download. So here it is. Data was created as described here: 

Edit: I had to write some quite hacky code around the download function to also have it be automatically downloaded during CI/CD. Theoretically, that entire part should be refactored because it's (unnecessarily complicated)**3, but time yada yada

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `701d58550551`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.