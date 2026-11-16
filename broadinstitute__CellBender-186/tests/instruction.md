# Issue

**Title:** Add BatchNorm to decoder

## Description

After several rounds of testing, found that BatchNorm in the decoder (but not encoder) seems to be beneficial (slightly) in terms of both smoothness of the learning curve and in terms of the latent representations.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d247426334c7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.