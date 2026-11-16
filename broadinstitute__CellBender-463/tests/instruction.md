# Issue

**Title:** Revamp benchmarking via github actions

## Description

This implements the benchmarking suite as a github action rather than a manual process which I often forget how to do.  This should make the whole repo easier to maintain and change confidently.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c5f5d9f41a29`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.