# Issue

**Title:** Add ModuleScore.StdAssay

## Description

In this PR:

1. Refactors `AddModuleScore` into an S3 generic
2. Adds a new `AddModuleScore.StdAssay` implementation that will iterate through layers and compute module scores separately on each layer
3. Adds a new test for the multi-layer case

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `38d354c2c8c7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.