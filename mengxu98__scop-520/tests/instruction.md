# Issue

**Title:** chore: synchronize documentation and local dependency lockfile

## Description

Synchronize the remaining generated documentation and namespace formatting, and apply formatting-only updates to SCENICPlus helpers. Refresh the lockfile to match the installed local environment, including Seurat 5.6.0 and its RcppThread dependency.

Validation: normalized SCENICPlus expressions and imported namespace symbols are unchanged; all seven affected Rd files pass parsing and documentation checks; `renv::status()` reports a consistent project; `git diff --check` passes. No CI workflow changes are included.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ab3989ace018`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.