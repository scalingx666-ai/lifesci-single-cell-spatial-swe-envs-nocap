# Issue

**Title:** [Backport release 2.3][ci] Temporarily disable remote tests

## Description

Disable remote storage workflow on PR/push until the tokens are updated.

(cherry picked from commit 7a6fb0c2463ee351cdf56985a10a7a048a60ae7e)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f11da4da2c56`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.