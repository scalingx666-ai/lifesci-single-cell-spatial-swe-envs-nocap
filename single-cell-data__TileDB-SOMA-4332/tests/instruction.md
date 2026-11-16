# Issue

**Title:** [Backport release-2.2] [r/ci] Replace P3M Bioc Mirror

## Description

Backport ac5e0c597f14449d0f841fc66a5651612aaab9b7 from #4302.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0ab9dc1b9ea1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.