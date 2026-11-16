# Issue

**Title:** Updating to `accelerate==1.14.0`

## Description

Reason: [a fix for avoiding double-wrapping in 1.14.0](https://github.com/huggingface/accelerate/blob/v1.14.0-release/src/accelerate/accelerator.py#L2067)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a7ccc0ddd9e7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.