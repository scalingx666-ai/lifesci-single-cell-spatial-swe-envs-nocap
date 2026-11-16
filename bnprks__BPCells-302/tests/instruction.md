# Issue

**Title:** [r] export `write_insertion_bed()`, clean up `write_insertion_bedgraph()` docs

## Description

Addresses #301

Also noticed that some old examples from `write_insertion_bedgraph()` were not update to accomodate the changes in normalization param names.  These are now fixed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b0be7e792bf7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.