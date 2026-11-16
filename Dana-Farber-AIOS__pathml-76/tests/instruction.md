# Issue

**Title:** Train hovernet

## Description

Created a notebook where I train HoVer-Net from scratch.
I'm intending that this will be a reference for users who want to train their own models (how to write training and eval loops in PyTorch, etc.).
It also benchmarks HoVer-Net performance, and now we can use the trained HoVer-Net for downstream tasks.
The model params are too big to put in the repo, so I'll open a new issue for that.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5245b62a0071`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.