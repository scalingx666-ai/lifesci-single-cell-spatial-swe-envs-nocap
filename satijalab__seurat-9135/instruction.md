# Issue

**Title:** Fix/load xenium

## Description

Updates `LoadXenium` to accommodate datasets without "Blank Codeword" or "Unassigned Codeword" matrices. Relates to:
- 

Cherry-picked from:
- 

Big thanks to @jsicherman for implementing the fix 🙏

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dcc012450173`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.