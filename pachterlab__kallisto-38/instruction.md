# Issue

**Title:** Devel

## Description

Adds option of specifying multiple FASTA files for index creation.
Processing single end reads has to be specified via a --single options.
Allows for processing multiple FASTQ files.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d6999173a2af`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.