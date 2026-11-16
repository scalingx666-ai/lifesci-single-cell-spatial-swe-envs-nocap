# Issue

**Title:** Minor `combineTCR` fix & refactor `combineBCR`

## Description

Switched back to using the `$barcode` syntax for selecting the barcode column instead of assuming its in the first position. Encountered this issue when working with a custom version of the data I manipulated.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b945dc14f19a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.