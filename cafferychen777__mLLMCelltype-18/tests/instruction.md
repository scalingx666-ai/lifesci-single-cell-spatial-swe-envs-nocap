# Issue

**Title:** Resolved the issue of inconsistency between the international version…

## Description

… and the mainland version of qwen.

Qwen's mainland version and international version use different URLs, add a rollback mechanism, when the Qwen international version does not work, rollback to the mainland version.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `30c8a0a64461`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.