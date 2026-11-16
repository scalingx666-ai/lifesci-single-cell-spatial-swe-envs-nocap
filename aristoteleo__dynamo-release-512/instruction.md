# Issue

**Title:** Update sctransform recipe

## Description

- Modified sctransform function and recipe. Now sctransform will only be performed on adata.X. Other layers will get normalized by size factors by default. 
- Users can run the sctransform on all layers manually, this will raise a warning.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a9b39580733c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.