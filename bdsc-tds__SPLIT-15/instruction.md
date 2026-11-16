# Issue

**Title:** Fix all-zeros profiles in SPLIT-shift

## Description

Fix bug where cells labeled as 'raw' but swapped according to SPLIT-shift were incorrectly assigned the residual profile (raw - purified) instead of retaining the original profile.
Solve issue #14.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d5668a45f17f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.