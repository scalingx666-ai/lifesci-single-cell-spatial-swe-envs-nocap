# Issue

**Title:** don't augment test or valid splits for PanNuke

## Description

Corrects behavior in PanNuke datamodule by not applying augmentations to test or validation dataloaders.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `eb122b688aeb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.