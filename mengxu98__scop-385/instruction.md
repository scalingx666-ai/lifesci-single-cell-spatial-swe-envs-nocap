# Issue

**Title:** fix: index Seurat workflow helpers in pkgdown

## Description

## Summary
- add the seven Seurat-compatible exports introduced by #384 to the pkgdown reference index

## Validation
- `pkgdown::build_reference_index()` completed successfully
- `git diff --check` passed

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `41aab74cea44`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.