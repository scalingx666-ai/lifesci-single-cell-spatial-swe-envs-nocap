# Issue

**Title:** Speed up paired end umi deduping

## Description

There is currently a bug with tid not actually fetching just the chromosome of interest in pysam.  This slows down the deduping for files with large amounts of contigs.  At least on my computer if you fetch via tid, all the reads get fetched (issue ).  While we wait for that bug to get fixed, I fixed this issue by removing tids from the code using the chromosome name instead.

This fixes issue  that I created.

Is there any testing or QC you'd like to me run before accepting this, let me know, I haven't done anything yet.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a4a55ee811d4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.