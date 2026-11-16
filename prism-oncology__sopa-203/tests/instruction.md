# Issue

**Title:** Baysor parallelization per patch

## Description

This adds parallelization to Baysor within each patch. See the Baysor docs here: https://kharchenkolab.github.io/Baysor/dev/configuration/

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c6473d0b4edf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.