# Issue

**Title:** Adding null support for query condition in SOMA queries

## Description

**Issue and/or context:**
Support for null test query conditions was added to TileDB core earlier this year and we haven't yet plumbed through support to TileDB-SOMA.

**Changes:**
- Adding `init_null` in tiledbsoma PyQueryCondition
- Adding unit test for `None` value inside a query condition

**Notes for Reviewer:**

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e552aee7ef2d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.