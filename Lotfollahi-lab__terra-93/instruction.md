# Issue

**Title:** Add gradient clipping and fix scaling with bfloat16

## Description

Add gradient clipping and scaling code from V-JEPA.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `44781ab0b8e5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.