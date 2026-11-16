# Issue

**Title:** fixed tarball wrong save name

## Description

When specifying another name than the default using the --checkoint flag the file still got saved to the default, effectively not allowing any cellbender instances to run concurrently. This fixes the issue.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `04c2f5b46072`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.