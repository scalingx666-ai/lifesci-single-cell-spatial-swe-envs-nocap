# Issue

**Title:** Feature-add / bug fix: allow annot.by = 'ident' in dittoHeatmap for Seurat objects

## Description

Per an emailed support question, users may expect `annot.by = "ident"` to work in `dittoHeatmap()` for Seurat objects, for pulling and annotating by clustering.

This PR adds this feature / fixes this perceived bug.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `727304c42a26`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.