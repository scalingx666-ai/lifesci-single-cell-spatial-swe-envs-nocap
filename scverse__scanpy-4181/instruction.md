# Issue

**Title:** Backport PR #4178 on branch 1.12.x (fix: masked cells were accidentally added to group 0 + mask ignored in aggregate computations in `get.aggregate`)

## Description

Backport PR #4178: fix: masked cells were accidentally added to group 0 + mask ignored in aggregate computations in `get.aggregate`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `82b91c588559`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.