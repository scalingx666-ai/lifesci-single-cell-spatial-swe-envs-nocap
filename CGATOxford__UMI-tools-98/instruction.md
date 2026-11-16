# Issue

**Title:** added sort to group directional so that correct representative UMI is…

## Description

… selected. Tested by comparing outputs minus the corrected UMI (BX tag in sam, 6th column in tsv). Thus the UG is the same even if the BX is different. Have replaced tests

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5772885fedfb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.