# Issue

**Title:** Update gtfparse version requirement

## Description

In 00ece88, `gtfparse` version was pinned to <2 because of confilcts between `gtfparse` and recent versions of `polars`. Since 12/21/23, with `gtfparse` v. 2.1.0, the conflicts have been eliminated, so there is no need to keep older versions pinned.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7badb5c884ee`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.