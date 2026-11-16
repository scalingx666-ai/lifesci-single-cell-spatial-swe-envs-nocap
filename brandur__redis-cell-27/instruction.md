# Issue

**Title:** Switch from crate `gcc` to `cc`

## Description

Apparently the former is now deprecated and the use of `cc` is
recommended now.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `974eb0203e1c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.