# Issue

**Title:** Conserve zero-shot prototypes when re-computing representations

## Description

Computing representations in zero-shot mode updated the prototypes.

Until now, it has not preserved the updated prototype for future runs (e.g., if we save and reload the model and re-run compute_representation without zero_shot).

Now, it updates the prototypes, and the model acts as a trained model

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0332e07a0d01`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.