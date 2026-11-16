# Issue

**Title:** properly pass image_resolution argument to mesmer model

## Description

The image_resolution argument is not utilized. This change passes image_resolution to the mesmer model through image_mpp (see: https://deepcell.readthedocs.io/en/master/API/deepcell.applications.html#deepcell.applications.mesmer.Mesmer).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b2eca9ed02e9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.