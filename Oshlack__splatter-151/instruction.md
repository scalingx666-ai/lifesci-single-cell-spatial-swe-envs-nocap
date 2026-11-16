# Issue

**Title:** Issue # 149 bug fixes

## Description

- fix Row.names vs rownames bug
- catch and correct batch.size parameter mistake where batch.size is > # samples

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a963d8d806e3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.