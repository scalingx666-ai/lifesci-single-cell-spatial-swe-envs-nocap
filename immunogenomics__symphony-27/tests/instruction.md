# Issue

**Title:** Move some plot-"enhancing" packages to Suggests

## Description

This fork was useful when trying to install symphony on the local HPC, to avoid a libcairo dependency.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0e93b270fdcb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.