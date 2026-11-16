# Issue

**Title:** [Backport release-3.0] [r] Fix resume-mode writes to new/empty arrays

## Description

Backport 6a59c3ef42df855e172f18836eec041d4d8fba40 from #4453.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `df363d7a697d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.