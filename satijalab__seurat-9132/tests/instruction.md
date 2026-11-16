# Issue

**Title:** Fix/read xenium

## Description

Resolves:
- 

by passing `simplify = FALSE` to the `sapply` call inside `ReadXenium`. Cherry-picked from:
- 

Big thanks to @alikhuseynov for implementing the fix 🙏

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b124c612db2d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.