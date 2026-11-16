# Issue

**Title:** changing assay to not be hard coded

## Description

DefaultAssay is hard coded in the fastCNV_10XHD function which results in an error when trying to run the function using a different assay. Changing this to the assay option of the function fixes this.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9c7f85ff08a6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.