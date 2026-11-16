# Issue

**Title:** add magic with reverse norm order

## Description

Reversing the order of sqrt and libnorm inexplicably improves performance. Adding this to MAGIC with explicit naming so users are aware that this is different from defaults.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8d90bc527f1d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.