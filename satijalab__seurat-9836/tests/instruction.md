# Issue

**Title:** Fix FindSpatiallyVariableFeatures

## Description

This PR updates `FindSpatiallyVariableFeatures` to get the method working again by:

- Updating `FindSpatiallyVariableFeatures.StdAssay` to point to `FindSpatiallyVariableFeatures.Assay`
- Deprecating the `slot` parameter in favor of `layer`
- Making sure that the matrix (typically `scale.data`) used by the underlying svf method contains only the relevant cells/features for the specified assay, image, and layer

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `985f3ec73104`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.