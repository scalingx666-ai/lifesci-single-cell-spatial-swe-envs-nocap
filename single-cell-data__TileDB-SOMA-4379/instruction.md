# Issue

**Title:** [Backport to release-2.3] [r] Test coverage for duplicate key behavior in SOMA collections

## Description

* Test write_soma throws existingKeyWarning

* SOMACollection tests for duplicate key handling

* Update expected error for duplicate key handling

* Verify original child wasn't replaced

* Add tests for duplicate handling across sessions

* Prevent replacing existing keys across write sessions

* Update NEWS.md

* Update SOMACollection docs

* Remove empty line



---------


(cherry picked from commit 29ef58af0cd8dfdd2c909470155ea7d549f3fc75)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `369996ca343d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.