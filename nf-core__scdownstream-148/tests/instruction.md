# Issue

**Title:** Improve integration parametrization

## Description

This PR allows users to:

- Specify categorical and numerical covariates for scVI and scANVI integration
- Improve parameterization of HVG selection

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ff4fe6bfd627`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.