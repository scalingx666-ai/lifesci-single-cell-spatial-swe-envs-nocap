# Issue

**Title:** Include `Cargo.lock`

## Description

Include `Cargo.lock` as requested in #75.

I think I originally omitted it so that no one was stuck to specific
dependency versions that really didn't make any difference whatsoever,
but I guess that's not that big of a problem, and the lock file has some
nominal benefit for reproducibility/security.

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `769d908d68a1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.