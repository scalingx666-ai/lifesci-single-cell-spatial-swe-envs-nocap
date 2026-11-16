# Issue

**Title:** Adaptor class for trvae

## Description

This adds adaptors for trvae.
I still need to add docstring and docs for Adaptor class.

Also, @M0hammadL, what is the intended behavior when an adaptor has a condition which is also present in the model to attach. Now it replaces weights for existing conditions with its adaptor's weights (if they are present in the adaptor). Is it the right behavior?

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `07af6bb4549e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.