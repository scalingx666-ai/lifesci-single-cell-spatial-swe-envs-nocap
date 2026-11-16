# Issue

**Title:** change labels_key to region_key

## Description

This PR fixes a small remaining issue due to a previous change of `labels_key` in `layer.metadata` to `region_key`. Due to hardcoding in the tests the tests for this change passed. However, this was not appropriately changed throughout the code base. While this PR quickly fixes this issue, our tests require a refactor to test the interaction between different widgets.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3ac24b551abe`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.