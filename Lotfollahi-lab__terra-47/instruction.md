# Issue

**Title:** fix a minor bug inside masking

## Description

While working on a new attention strategy, I found a minor bug in the masking, which essentially drops tokens from both the cell and neighbor in the size of n_special_tokens. This causes the last two tokens of the cell and neighbor to be excluded from the masking if n_special_tokens is set to two (for example, when adding two CLS tokens). Although this shouldn't affect the results, it's still good to fix it.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `992abeb5f8c4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.