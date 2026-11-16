# Issue

**Title:** [Backport release-2.3] [r] Skip tests using deprecated code in envs with lifecycle < 1.0.5

## Description

Backport 6173f240e59a446538f07e007d4789e1f0057b9b from #4395.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `da72c648b305`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.