# Issue

**Title:** Back-merge the 4.0.3 security patch into dev

## Description

Forward-ports the merged `master` security patch into `dev` so the fix is a shared ancestor and the coming removal of the momentarily ignored lint tests (coming with nf-core/tools 4.1.0) propagates cleanly.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a9c500ee2122`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.