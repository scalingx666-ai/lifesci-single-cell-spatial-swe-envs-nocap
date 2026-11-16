# Issue

**Title:** use lambda expression in Hnsw::NormalizeVector

## Description

* CRAN complains about `std::bind1st` as it has been deprecated. So, this replaces `std::bind1st` with a lambda expression.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `27d4e278143d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.