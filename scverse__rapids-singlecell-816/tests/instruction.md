# Issue

**Title:** ci: add skip-gpu-ci label

## Description

Adds a `skip-gpu-ci` label that makes the GPU CI gate jobs (`CI-Pass`, `All Tests Green`) pass without running the GPU tests, for PRs that cannot affect GPU code.
`run-gpu-ci` and pushes to `main` still take precedence, so labeling a PR never hides a requested GPU run.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `488fbe51f708`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.