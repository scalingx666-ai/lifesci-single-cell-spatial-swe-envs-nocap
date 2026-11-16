# Issue

**Title:** Allow future HF organization name

## Description

Currently, when loading a model with `from_pretrained`, it breaks if the organization name is not `MICS-Lab`. In the future, the org will be renamed, so this PR aims to already accept the new org name to prepare for the future change.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `67c407ef95a4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.