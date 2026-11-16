# Issue

**Title:** subsetLiger and reorganizeLiger changes

## Description

Hi Liger Team,

This PR implements changes mentioned in #180 to address `subsetLiger` object when a dataset only contains a single cell and #181 to implement a check in `reorganizeLiger` in case cell.data feature is not a factor.

Best,
Sam

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7c8b7c6ecff7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.