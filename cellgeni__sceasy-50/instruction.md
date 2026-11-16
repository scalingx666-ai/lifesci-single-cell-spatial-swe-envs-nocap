# Issue

**Title:** Code clean up

## Description

This PR introduces the following changes to serve as basis for further functionality additions:

1. Drop dependency on "loom_utils.R" and relax anndata version requirement
2. Add function docs
3. Use tidyverse code style.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `57cada717e0a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.