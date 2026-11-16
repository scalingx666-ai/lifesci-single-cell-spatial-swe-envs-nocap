# Issue

**Title:** Feat/no internet

## Description

Allow usage of SeuratData even when offline 
 - Now caches data manifest
 - Includes bundled manifest for when no cache is present
 - Simplify data package key

Addresses #2

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e6bab092c71c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.