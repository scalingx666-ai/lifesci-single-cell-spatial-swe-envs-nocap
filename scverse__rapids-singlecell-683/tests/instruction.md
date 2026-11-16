# Issue

**Title:** add wasserstein to pertpy GPU Distance

## Description

This adds the Wasserstein metric to pertpy-GPU Distance. For larger Dataset this is up to 400x faster than Pertpy using Jax-GPU. It also fixed an issue with empty categories for edistance

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `63242283131b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.