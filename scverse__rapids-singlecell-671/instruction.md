# Issue

**Title:** harden cooc for atera

## Description

co_occurrence can overflow for very large datasets like Atera.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `282e207a2f8f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.