# Issue

**Title:** [Backport release-2.3] [python] Pin pandas to be less than 3.0.0

## Description

Backport ac64a7fa17139cc546bf37c274ffbec022fdcb35 from #4382.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9bd9dbb6009b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.