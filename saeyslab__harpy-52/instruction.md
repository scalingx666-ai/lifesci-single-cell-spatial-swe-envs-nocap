# Issue

**Title:** Sc 25 custom aggregate

## Description

- support for custom aggregation of mask and image using a custom function that can not be scaled using map_blocks.
- todo: support of extraction of multiple feature in one pass over masks and image

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fcdad003421a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.