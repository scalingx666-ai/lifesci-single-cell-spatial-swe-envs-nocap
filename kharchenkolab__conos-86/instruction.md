# Issue

**Title:** replace std::bind1st with lambda expression,  Hnsw::NormalizeVector

## Description

* CRAN complains about `std::bind1st` as it has been deprecated. This is meant to replace `std::bind1st` with a lambda expression.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `345d6ebe7c3a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.