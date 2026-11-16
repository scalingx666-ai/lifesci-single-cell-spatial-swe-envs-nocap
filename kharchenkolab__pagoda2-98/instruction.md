# Issue

**Title:** Bugfix, check list elements exist within serializeToStaticFast(), WriteListToBinary()

## Description

This is currently my best attempt to address  though I haven't been able to replicate this bug myself.

Naturally, I'm guessing there are more checks we could do to make sure that what's fed into WriteListToBinary() will be formatted correctly. 

* check list elements exist in `exportList`, which is fed to `WriteListToBinary(expL=exportList, ..)`. If name doesn't exist, throw error.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8a0e3608b952`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.