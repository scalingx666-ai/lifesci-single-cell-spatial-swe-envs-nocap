# Issue

**Title:** change back to original matplotlib backend

## Description

When using the UMI-tools API only, I noticed it switches my Matplotlib backend to Agg, which messes with the plots I generate downstream. This PR changes the backend only when generating plots and then switches back to the user's original setting

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7e799bc120f1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.