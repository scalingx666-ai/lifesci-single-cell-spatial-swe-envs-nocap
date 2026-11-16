# Issue

**Title:** Simplify Embedding of novel species

## Description

This PR simplifies the process of embedding novel species not seen in the training set by adding a csv config file where they can be specified (after running through the creation notebook).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e6cb916f0070`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.