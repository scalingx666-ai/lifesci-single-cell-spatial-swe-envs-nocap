# Issue

**Title:** Tkakar/fix 2582 annotation multiple properties

## Description

Fixes two upstream bugs in the bundled Neuroglancer that caused incorrect rendering of multi-property, multi-resolution annotation datasets:

- int8 serialization size bug — serializedBytes() returned 2 instead of 1 for int8 properties, causing "Expected X bytes, but received Y bytes" errors for any schema with int8/uint8 properties. Fixed upstream in ; this patch backports it. 
Without this fix the points are not showing up and a byte mismatch error is thrown.

- Missing epsilon tolerance and chunk-index clamping in updateFixedCurPositionInChunks — floating-point rounding could push a computed chunk index out of bounds for a given spatial resolution level (each level has a different chunkSize), causing some levels to silently resolve to the wrong chunk. With multiple resolution levels active simultaneously, this produced visibly duplicated/offset point clusters for the same physical region.

 
Closes hms-dbmi/tissue-map-tools#45
<!-- For other PRs without open issue -->
#### Background
<!-- For all the PRs -->
#### Change List
-
#### Checklist
 - [ ] Have tested PR with one or more demo configurations
 - [ ] Documentation added, updated, or not applicable

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `49b8bbf76981`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.