# Issue

**Title:** Fix exception due to adata being none

## Description

CI is red because of this: 

The PR fixes two exception that originated when an annotating table `adata` was `None`. I discovered this bug with this code snippet:

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `602db3c97fe6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.