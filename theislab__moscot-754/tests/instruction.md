# Issue

**Title:** Fix sankey threshold

## Description

@753

Fixes the threshold argument in `TemporalProblem.sankey`

Before:
![sankey_without_th](https://github.com/user-attachments/assets/22b201b0-7b95-450c-8558-a0600f573c00)
After:
![sankey_with_th_ 05](https://github.com/user-attachments/assets/fe1ef22e-64b5-48cc-8dfd-75d5b76596a4)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ba8d30f045a5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.