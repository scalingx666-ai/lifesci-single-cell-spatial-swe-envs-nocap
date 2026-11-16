# Issue

**Title:** Fixed feature subsetting in PrepDR5

## Description

To fix GitHub issue #8627 -- previously, `RunPCA` incorrectly discards features if any zero-variance features are present, due to improper subsetting. This is now fixed through a simple modification to `PrepDR5`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d464e640cf30`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.