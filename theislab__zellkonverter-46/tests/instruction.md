# Issue

**Title:** Began adding an R-native reader for H5AD files.

## Description

This creates an R-native reader that directly uses **rhdf5** and other BioC packages to read H5AD files. The general idea is to reduce the level of reliance on the **basilisk** bindings for the 95% of use cases, avoiding the various issues with Python communication; but still retain our current **basilisk** infrastructure as a fallback for difficult and weird cases.

Seems to work fairly well though some more testing is needed. Code is also required to handle `uns`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `50ba4c11ba0f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.