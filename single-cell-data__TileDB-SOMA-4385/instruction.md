# Issue

**Title:** [Backport release-2.3] [r] Add Carrara test coverage for duplicate key behavior

## Description

Backport 71e9cb989d2e4137539231e64d02b2ab4281f945 from #4384.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9bd9dbb6009b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.