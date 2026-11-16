# Issue

**Title:** Naming of output directory structure

## Description

This PR changes the naming of the output directory structure in several levels, but mostly moves the directory structure specification from being defined in some processes to the config instead, as well as adding more descriptive subdirectories for the final output.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a3899deccfb8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.