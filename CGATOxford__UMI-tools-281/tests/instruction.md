# Issue

**Title:** {ts} debug missing tag

## Description

This enables reads missing a UMI or CB tag to be skipped rather than throwing an error ().

As part of this, I've also moved the check for UMI/CB tags to before the check for bundle yielding as per all the other checks which cause reads to be skipped.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e757f8889b08`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.