# Issue

**Title:** Refactor SCTransform.StdAssay

## Description

This PR simplifies the implementation of `SCTransform.StdAssay` so that it:
- Takes each input layer and instantiates a new v3 `Assay`
- Passes each intermediate assay to `SCTransform.Assay` and then merges the output
- Updates the features in the merged output's `scale.data` slot to be the intersection of all variable features that are also present in all individual outputs
- Sets the merged output's variable features

This PR also fixes `merge.SCTAssay` to avoid throwing an error when passing assays containing multiple models.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5928f1838c3c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.