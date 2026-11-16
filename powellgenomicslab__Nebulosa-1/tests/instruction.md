# Issue

**Title:** Use Seurat accessors instead of slot

## Description

Replaces calls to `slot` with `Seurat`-object accessor functions and methods
- Checks if a reduction name is in `Reductions(object)` (a vector of all dimensional reductions in the `Seurat` object)
- Pulls cell embeddings with `Embeddings(object[[reduction]])` (`object[[reduction]]`, is short-hand for pulling a dimensional reduction)
- Gets the metadata dataframe with `object[[]]` (leaving `[[` empty pulls the metadata dataframe)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e46cec1f87dd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.