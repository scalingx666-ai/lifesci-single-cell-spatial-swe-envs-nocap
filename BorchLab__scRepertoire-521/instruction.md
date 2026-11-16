# Issue

**Title:** Expanding Unit Tests

## Description

Aimed at expanding unit tests for: 

- ```combineExpression()``` and changing the <1% warning to an error
- ```loadContigs()``` adding TRUST4 and auto format detecting
- ```StartracDiversity()``` adding pairwise functionality unit tests.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `29b33992fe70`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.