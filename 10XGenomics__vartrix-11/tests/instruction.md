# Issue

**Title:** Validate sequences.

## Description

Check every VCF record for having a sequence present in the BAM and the FASTA. This will prevent cryptic errors.

For issue #7.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `152a0b3ad4b4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.