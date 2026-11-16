# Issue

**Title:** Clean SegmentMIF

## Description

#293 Tensorflow devices should not be configured in SegmentMIF, they should be managed by the user

Correctly pass pre/postprocess_kwargs arguments to predict

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `65ecf6c47fd3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.