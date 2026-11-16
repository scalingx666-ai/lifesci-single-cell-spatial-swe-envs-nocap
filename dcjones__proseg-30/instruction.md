# Issue

**Title:** missing gene-column error fix

## Description

Change error message with missing gene-column to "Missing required argument: --gene-column" instead of "Missing required argument: --transcript-column"

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `90957b1105f7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.