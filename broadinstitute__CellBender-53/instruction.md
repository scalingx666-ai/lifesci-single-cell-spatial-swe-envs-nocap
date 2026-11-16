# Issue

**Title:** Bug fix for large transcriptomes: uint16 overflow

## Description

There was a bug that slipped past my notice until now:

I was using `uint16` to store gene indices for output sparse count matrices (after what I saw CellRanger doing back in early version 2).  This is a bad idea, especially for mixed-species datasets, and for newer v3 datasets which tend to just have larger transcriptomes (> 65k).  The result was a mangled output, where the count matrix would be missing some genes entirely, and their counts would be assigned to other genes.

Updating `uint16` -> `uint32` solves the problem.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d68bf9dd2785`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.