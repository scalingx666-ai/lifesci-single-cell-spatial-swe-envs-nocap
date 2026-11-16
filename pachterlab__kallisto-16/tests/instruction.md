# Issue

**Title:** Range

## Description

Adds more info for the matching of the reads.

A parameter min-range (default value of 2*k+1) determines whether to accept the match or not, once we've found the intersection of ECs.

The range is found by taking the max and min of the positions of k-mers within the read and adding k. The k-mer positions for the second pair (on the reverse strand) is modified to be

(fld-k)-pos

where fld-k is the position of the last k-mer in the fragment. So if we have two supporting k-mer on either read they provide better evidence than a two adjacent k-mers within the same read.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b2bc47f44b29`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.