# Issue

**Title:** Fix linking to RcppParallel

## Description

To link to RcppParallel you need to set PKG_LIBS. Otherwise it won't work reliably.

Fail log: https://github.com/r-universe/yulab-smu/actions/runs/7490624182/job/20390858995

Examples from other packages: https://github.com/search?q=org%3Acran%20path%3Asrc%2FMakevars%20RcppParallel%3A%3A&type=code

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6948939686ea`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.