# Issue

**Title:** Added command line flag --ignore-tlen

## Description

Added command line flag --ignore-tlen, an option to dedup paired end reads based solely on read1, whether or not the template length is the same.

Added a test for the --ignore-tlen flag.

Original issue:

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5e99b633932d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.