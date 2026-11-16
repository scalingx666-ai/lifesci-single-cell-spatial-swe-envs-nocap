# Issue

**Title:** Fix parsing NA value of text annot in ColorMesh

## Description

When pass text for heatmap annot, error with `TypeError: ufunc 'isnan' not supported for the input types, and the inputs could not be safely coerced to any supported types according to the casting rule ''safe''`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8a9d087e48e1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.