# Issue

**Title:** Remove `.drop` argument

## Description

Hi there, we are working on the next version of dplyr and your package was flagged in our reverse dependency checks.

We've advanced our deprecation of the `.drop` argument of `add_count()` which was deprecated in dplyr 1.0.0 and is now defunct.

dplyr will be released on January 31, 2026. If you could please send an update of your package to CRAN before then, that would help us out a lot! Thanks!

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `84ccbfc470c4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.