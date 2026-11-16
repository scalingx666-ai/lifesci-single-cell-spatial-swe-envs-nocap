# Issue

**Title:** Fix bug with unmapped paired end reads

## Description

It seems that for paired end reads where the second read of each pair is unmapped, they are not discarded when the option for handling unmapped reads is to discard them. I'm not entirely sure whether this is intended behavior, but it likely isn't and the code has a typo.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e3251182d9a4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.