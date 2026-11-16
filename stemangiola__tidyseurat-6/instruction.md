# Issue

**Title:** Update README & GHA

## Description

Noticed the vignette was updated but the README wasn't so updated it here. You still have to do a Knit of the README.Rmd to update the README.md if you change the man/fragment/intro.Rmd.

By the way what do you think now that it's incorporated,, is the man/fragements shared content vignette/README ok for you?

Also modified the GHA to autodetect the current Bioc release to test against instead of hardcoding the version. So it tests against 3.11 now & will autodetect Bioc 3.12 when it's released next month.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ec3d342465ee`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.