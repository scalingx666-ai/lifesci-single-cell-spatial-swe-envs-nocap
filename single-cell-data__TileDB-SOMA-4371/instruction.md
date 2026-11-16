# Issue

**Title:** [Backport to release 2.3]  [python] Add function to cast for old versions of pyarrow (#4367 )

## Description

Add function to cast for old versions of pyarrow that do not yet have `RecordBatch.cast` implemented.

(cherry picked from commit d309274d098aa3ed0dd1ed7a18f4b313d8763982)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fd3ebaf16542`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.