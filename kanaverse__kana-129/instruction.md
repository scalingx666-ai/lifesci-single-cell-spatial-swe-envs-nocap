# Issue

**Title:** Moved param translation to/from UI/bakana into its own file.

## Description

This will allow for easier vendoring into related applications such as
kanapi. Also minor fixes for the new ADT-related steps.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b94c12cf4049`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.