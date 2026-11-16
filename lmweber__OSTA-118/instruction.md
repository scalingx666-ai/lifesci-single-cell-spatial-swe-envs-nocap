# Issue

**Title:** gene/feature-set signatures draft

## Description

ping #54 - currently covering signature scoring (using `AUCell` (a.k.a. SCENIC). Next iteration might want to include something like MOFA/gene set enrichment analysis, something with TFs, etc.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e34c253d6297`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.