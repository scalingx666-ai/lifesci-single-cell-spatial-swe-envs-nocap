# Issue

**Title:** Read suffixes removed from single end data

## Description

Moved code to remove "suffixes" from the first word of of the read identifier from joinedFastqIterate to fastqIterate.

Changed call of fastqIterate in extract to specify  whether to remove suffixes.

Should solve #580

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d98ebace3a09`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.