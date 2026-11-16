# Issue

**Title:** typo fix, reduce source package size

## Description

- fix typo flipping Cosmx/Xenium (#315)
- ignore ^inst/pages in .Rbuildignore (#316)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ca9ebaa54a1e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.