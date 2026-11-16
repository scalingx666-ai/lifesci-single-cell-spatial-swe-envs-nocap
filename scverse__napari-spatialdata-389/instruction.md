# Issue

**Title:** Fix docs links

## Description

Some links were still pointing to the old S3 storage location. Thanks @artur-man for reporting.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6747bf035d79`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.