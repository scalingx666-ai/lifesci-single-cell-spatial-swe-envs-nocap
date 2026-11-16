# Issue

**Title:** Fix inputs handler to be amenable to serialization

## Description

Because it currently isn't.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ced5229f5b5b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.