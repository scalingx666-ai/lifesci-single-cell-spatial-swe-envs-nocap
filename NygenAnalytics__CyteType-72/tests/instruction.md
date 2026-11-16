# Issue

**Title:** Update version to 0.19.3 and enhance gene symbol handling

## Description

- Bump package version to 0.19.3.
- Introduce materialization of a canonical gene symbols column in AnnData, improving gene symbol management.
- Refactor CyteType class initialization to handle gene symbols more flexibly, including support for temporary columns.
- Update `save_features_matrix` to conditionally include gene symbols metadata in output files.
- Enhance tests to validate new gene symbol handling and ensure proper functionality.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7a9b4a1d8083`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.