# Issue

**Title:** Install pkgdown with BiocManager

## Description

This should fix the fail. It's due to the actions trying to install pkgdown from Github that has a downlit dependency that's not available for the Bioc Docker release 3.11. Installing pkgdown with BiocManager fixes it.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1569c491698b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.