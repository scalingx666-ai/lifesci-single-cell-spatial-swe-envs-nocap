# Issue

**Title:** Strip fastq lines, rather than explicitly removing last char.

## Description

This should help if input file has DOS-like line endings, replacing them with UNIX ones.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2c0cecfea1b9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.