# Issue

**Title:** {ts} debug per gene

## Description

Resticts pysam fetch to transcripts actually observed in the BAM when using the --gene-transcript-map method

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cd652b425ee1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.