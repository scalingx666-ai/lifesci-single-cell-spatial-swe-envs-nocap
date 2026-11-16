# Issue

**Title:** Debug psl

## Description

When we have an array like `dist` input, `if not dist` will regard it as a check on multiple values and then raise an error. What we need is `if dist is None`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7a45dec76f63`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.