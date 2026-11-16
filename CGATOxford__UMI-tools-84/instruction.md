# Issue

**Title:** {ts} fix group

## Description

This fixes the group command so that each read is assigned to a single read only.  

I've done a basic check that the number of read groups outputted with _group_   ==  the number of reads  outputted with _dedup_

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `487ddc6b7984`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.