# Issue

**Title:** Added parameter to adjust the size of gene tags

## Description

Added a parameter called 'tag_size' to the function call for geom_repel_text / geom_repel_label. The parameter is set at a reasonable default, but larger than the original default for geom_repel.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `50551eeb10b3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.