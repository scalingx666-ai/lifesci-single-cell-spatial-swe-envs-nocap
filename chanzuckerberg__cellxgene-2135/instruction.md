# Issue

**Title:** propagate diffexp state through component tree

## Description

The differential expression state was not correctly being propagated through the component tree, which manifest as a missing "p-val" and "lfc" on histograms related to diffexp. This PR makes the state available to the components that actually need it.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ae30b66123f6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.