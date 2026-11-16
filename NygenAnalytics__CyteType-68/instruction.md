# Issue

**Title:** Update version to 0.18.1 and enhance public API formatting

## Description

- Bump package version to 0.18.1.
- Refactor __all__ in __init__.py for improved readability.
- Update gene ID regex in validation.py to allow for versioned gene IDs.
- Modify _id_like_percentage function to support random sampling with a seed for better statistical representation.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `27ae521a9d96`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.