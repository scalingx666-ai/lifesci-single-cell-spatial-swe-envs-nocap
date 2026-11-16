# Issue

**Title:** Stop SPLIT if RCTD is not post-processed

## Description

Add a validation check that verifies `SPLIT::run_post_process_RCTD()` has been applied to the RCTD object before proceeding, and throws an informative error with remediation instructions if not.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3cc79c823392`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.