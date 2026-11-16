# Issue

**Title:** [Backport release-2.0] [ci] Fix issue where we are unable to checkout tag

## Description

Backport 73dff5a6b53b802e3220976e5985def462383edf from #4255.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `48201fb699da`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.