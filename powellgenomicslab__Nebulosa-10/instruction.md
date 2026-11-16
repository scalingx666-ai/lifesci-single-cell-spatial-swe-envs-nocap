# Issue

**Title:** Replace Seurat imports with SeuratObject

## Description

Replaces all Seurat data access imports with SeuratObject and moves Seurat to Suggests
This should help decrease install time for platforms that utilize source installs as Seurat and all of its dependencies are no longer installed
All functionality remains intact; automated install of Seurat alongside Nebulosa can be achived by passing `dependencies = TRUE` to the install command

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4c795d798c12`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.