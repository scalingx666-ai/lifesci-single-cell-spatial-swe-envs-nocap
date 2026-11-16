# Issue

**Title:** add dependencies for `seq-workflow-visium-hd`

## Description

Namely, Bioc packages `SpotSweeper` and `Spatial`. (Note: This PR is meant to trigger the deps GHA in advance to PR #159)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `df54f0ef02ec`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.