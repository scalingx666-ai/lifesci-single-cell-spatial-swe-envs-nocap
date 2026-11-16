# Issue

**Title:** Redistribute counts

## Description

Allows to redistribute residual counts among spatial neighbors of the contaminating cell type if any. 

[An example](https://github.com/bdsc-tds/SPLIT/blob/redistribute-counts/vignettes/Reassign_residual_transcripts.Rmd)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a3cbddf40e0b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.