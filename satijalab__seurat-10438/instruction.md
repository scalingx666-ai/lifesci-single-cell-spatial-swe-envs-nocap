# Issue

**Title:** Fix handling of v5 objects inside `PercentageFeatureSet`

## Description

### Update `PercentageFeatureSet()` to properly access Seurat v5 layers

This had been reported on an old issue thread at  and resurfaced as an issue when running Azimuth 0.5.1 

The error at  occurs because the bracket subsetting `object[[assay]][layer]` misinterprets the layer name "counts" as a feature selector rather than a layer identifier.

We were already calling `LayerData`; this PR just moves that line up to before feature retrieval.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `258a250c7b27`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.