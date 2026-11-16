# Issue

**Title:** Properly handle distance metrics

## Description

##### Issue
Distance metrics had undefined behaviour i.e. it was up to the library to raise errors and handle everything.

##### Description of changes
- Use only distance metrics available in both nearest neighbour libraries and exclude the others. If it's not a valid distance metric, then an appropriate error is raised.

- Use ball tree instead of KD tree because it supports many more distance metrics.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dff1fe751aa4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.