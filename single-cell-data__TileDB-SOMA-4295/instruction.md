# Issue

**Title:** [r] Fix build when workspace path contains spaces

## Description

**Issue and/or context:** Building the R package fails in working direcories that contain spaces in their filepaths.

**Changes:** Quotes the `@cmake@` placeholder to prevent unintentional path splitting.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8af224955354`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.