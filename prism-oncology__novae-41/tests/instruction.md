# Issue

**Title:** Upgrade to new sopa version

## Description

In `sopa==2.2.0`, we now use `zarr v3`. While it shoudn't impact novae, this is a relatively big sopa update so we want to fully switch to this new version.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `853c290540ef`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.