# Issue

**Title:** Fix `Cells.SCTAssay` for `LeverageScore`/`SketchData`

## Description

This PR makes two changes:
1. Updates the `Cells.SCTAssay` method to allow "regular" layer names (i.e., `"counts"`, `"data"`, and `"scale.data"`).
2. Drops the call to the `VariableFeatures` setter at the end of `SketchData`.

The first update makes `SCTAssay` inputs compatible with `SketchData` and `LeverageScore`. The second change is mostly a speedup, but in this context also avoids a warning from `VariableFeatures.SCTAssay` about unused arguments. 

Resolves:
-

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `42be3db83e51`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.