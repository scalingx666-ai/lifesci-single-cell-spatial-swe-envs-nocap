# Issue

**Title:** Add nightly CI runs + wait for PyPi propagation before docker image build

## Description

and #342
CI scheduled at 00:00 on Monday, Thursday, and Saturday.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2e72abe4c036`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.