# Issue

**Title:** os.replace() instead of os.rename() to save checkpoint

## Description

Fixes Windows bug #250

Merging it into `sf_posterior_int_overflow` because I added a Windows github action test there, and the test fails without this fix.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `af80d5aa20d7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.