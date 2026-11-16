# Issue

**Title:** Fix PseudobulkExpression for multi-assay inputs

## Description

This PR fixes a bug with PseudobulkExpression encountered when passing in a `Seurat` object containing more than one assay.  The issue was that a single category matrix was being made at the object level, but it needs to be generated for each assay.

While I was in the neighborhood, I also dropped the `@importFrom SeuratObject .IsFutureSeurat` tag from the docstrings from `PseudobulkExpression.Assay`. The private `SeuratObject` method isn't actually used, and I'd like to drop it from the package so that I can remove the circular dependency with Seurat.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `103375fb7854`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.