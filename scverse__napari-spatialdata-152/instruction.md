# Issue

**Title:** Switch to currentItemChanged

## Description

For the `CoordinateSystemWidget` the only way to change was by clicking. This PR introduces a change so that the callbacks happen on `currentItemChanged`. This item can change based on click but also when using the arrow keys.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `27dca4168f31`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.