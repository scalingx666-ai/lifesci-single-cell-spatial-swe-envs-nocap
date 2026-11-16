# Issue

**Title:** crs-registrations

## Description

As mentioned during call, some chunks are not being evaluated, but most Voltron-specific things have been consolidated similar to "other methods" not being on CRAN/Bioc. relates to #153

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7841d1894f24`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.