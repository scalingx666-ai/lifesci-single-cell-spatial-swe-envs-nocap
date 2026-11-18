# Issue

**Title:** build: require scverse-doc 0.4

## Description

liana's crimson and turquoise are in scverse-doc's registry from 0.4.0, so the docs show them instead of the scverse blue, and math renders at build time with math-core.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `228ac2233564`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.