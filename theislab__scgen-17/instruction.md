# Issue

**Title:** stop batch correction cell index scrambling, and retain raw if present

## Description

added `index_unique=None` to concatenation, sorted `corrected` on `adata.obs_names` and copy over `.raw` from the original object if it's not empty.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `622415e69bdc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.