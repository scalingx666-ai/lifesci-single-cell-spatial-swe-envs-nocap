# Issue

**Title:** add gtf, fasta validation

## Description

* when FASTA and GTF chromosomes do not match
* when a GTF entry is not parsable
* when either `transcript` or `exon` entry for a transcript is missing in the GTF

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c0d4230e2d16`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.