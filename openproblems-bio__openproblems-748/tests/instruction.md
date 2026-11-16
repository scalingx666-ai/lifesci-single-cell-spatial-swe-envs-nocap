# Issue

**Title:** Fix PID checking

## Description

This was running in `sh` for some reason.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0854ee4c61fb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.