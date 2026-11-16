# Issue

**Title:** Fix index for multiple alpha/beta chains

## Description

I believe there was an incorrect index in the parseTCR utility function, which lead to TCR-beta chains reported as alpha chains. I flagged the line of the change with the comment ##HERE

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d02c508bed07`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.