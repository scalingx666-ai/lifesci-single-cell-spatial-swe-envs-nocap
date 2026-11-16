# Issue

**Title:** Replace defunct purrr::when()

## Description

🤖 Written by AI 🤖

purrr's next release makes `when()` defunct (it has been deprecated since purrr 1.0.0). Tests pass with both CRAN and dev purrr, so this can be merged and released independently of purrr's release.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5a96f9573251`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.