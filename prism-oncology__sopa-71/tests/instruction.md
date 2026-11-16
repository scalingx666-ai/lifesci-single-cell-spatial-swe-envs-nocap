# Issue

**Title:** WSI tile gathering optimizations

## Description

This PR improves the performance of tile gathering from the WSIs to about ~x7. Simplifies the codebase of `sopa.patches.infer`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5823fe26aa26`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.