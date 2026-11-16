# Issue

**Title:** [python] Additional deprecation removals schedules for the 3.0.0 release

## Description

**Changes:**

* Add a defunct section to R NEWS. We have a deprecate, defunct, and remove stage in our deprecation policy. Adding an explicit defunct header to the news helps make it more clear what the current state is.
* Remove resume ingest mode (deprecated in 1.18.0).
* Remove straggling delete-in-write-mode warning.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e7370592e019`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.