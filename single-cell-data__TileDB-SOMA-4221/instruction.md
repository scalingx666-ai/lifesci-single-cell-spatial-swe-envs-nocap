# Issue

**Title:** Move initial ArraySchema creation to platform config file

## Description

More code movement out of `arrow_adapter.h/cc`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5550c6f09563`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.