# Issue

**Title:** CRAN check resolve

## Description

1. Rd cross-references for formatting.Rd: tbl_format_setup
2. package dependencies for ‘SingleR’: remove it from DESCRIPTION as it is a non-CRAN package. We still mention/use them in vignettes conditionally by setting `eval=FALSE`

Tested locally, the above notes are resolved.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9f9d2187d380`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.