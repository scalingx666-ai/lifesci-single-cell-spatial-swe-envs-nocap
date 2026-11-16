# Issue

**Title:** [Backport release-2.2] [ci] Remove the ubuntu-src dockerfile

## Description

Backport 0b809a2b1a0d095c3fdfe741a65e55f2b2696c01 from #4308.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bc00cf0ccc7e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.