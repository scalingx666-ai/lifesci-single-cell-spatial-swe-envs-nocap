# Issue

**Title:** Removed leiden as hard dep to stay BSD3 compliant

## Description

This PR removes leidenalg as a dependency to avoid inadvertently imposing GPLv3 licensing on Squidpy. Keeping it as a hard dependency could force the entire package to comply with GPLv3, conflicting with Squidpy’s intended BSD license. Removing it ensures we maintain the correct licensing and avoid potential legal ambiguities.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0d5dfa92383e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.