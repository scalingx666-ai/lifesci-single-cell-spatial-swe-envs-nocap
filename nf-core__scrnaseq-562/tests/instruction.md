# Issue

**Title:** Fix/prepare genome optional fasta and gtf

## Description

Adresses . Fixes a regression that was introduced with the `PREPARE_GENOME` subworkflow, where the pipeline runs into errors when only an aligner index is provided, but not reference genome FASTA/GTF files

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dd77ed0f0a7a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.