# Issue

**Title:** Resolve TS lint added in previous PR

## Description

PR #2347 added a bunch of TS lint.   :disappointed:   This PR resolves it, partly with error suppression consistent with the current TS migration status.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8136387127a4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.