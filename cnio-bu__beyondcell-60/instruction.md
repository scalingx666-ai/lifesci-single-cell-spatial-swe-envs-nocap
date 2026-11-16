# Issue

**Title:** Fix GetCollections filters and default tests

## Description

Basically, the tests had bugs for the most part. On the other hand, we did catch a nasty issue in R/Basics.R, line 264 where MoAs were not mapped correctly.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a7f09496c6a1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.