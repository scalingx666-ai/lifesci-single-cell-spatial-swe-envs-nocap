# Issue

**Title:** Exclude unclustered cells from deciding doublets.

## Description

Unclustered cells receive 'np.NaN' for their score and p-value.

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `69aca5ebfa81`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.