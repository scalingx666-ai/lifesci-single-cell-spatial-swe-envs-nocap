# Issue

**Title:** Adds 'batch.rmEffect' parameter.

## Description

When the 'batch.rmEffect' is TRUE, the simulation randomly generates the batch effects to preserve the random seed, but then removes the batch effect by over-writing the generated batch effects by 1.

This allows creating simulation pairs with and without batch effects.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `497661db5fbe`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.