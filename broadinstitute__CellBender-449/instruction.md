# Issue

**Title:** suppress pandas warnings

## Description

New pandas version led to a ton of warnings during final noise count estimation.

Fix the problem by updating pandas syntax, thereby removing the warnings.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a558f6b0d683`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.