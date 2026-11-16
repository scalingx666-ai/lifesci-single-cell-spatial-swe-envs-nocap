# Issue

**Title:** Updates annotateInvariant function to support BiocParallel

## Description

Replaces lapply and vapply calls in annotateInvariant with bplapply calls accepting any BiocParallel parameter class. 
Adds BiocParallel to imports in DESCRIPTION. 
Adds test for parallel function matching single thread call. The test uses SnowParam which spins up very slowly so it is longer than single thread compute, but it should work on all BioC build environments.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a7f3953f2c38`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.