# Issue

**Title:** Infer backend from path

## Description

This changes the logic used to infer the correct backend to use for a given file path. Instead of trying to parse the file extension and then matching it to our lists of supported file extensions, this loops through our list of supported file extensions and checks whether they match the given file path. Also added some test cases to cover what was failing before.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b2eca9ed02e9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.