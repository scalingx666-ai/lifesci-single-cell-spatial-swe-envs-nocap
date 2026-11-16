# Issue

**Title:** Adds normalizer parameter.

## Description

Allows specifying the normalizing function to use on raw_counts.
Defaults to included normalize_counts, the previously always-used function.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1dfef065f60b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.