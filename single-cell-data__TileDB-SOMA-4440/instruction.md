# Issue

**Title:** [python] Set the context in spatial import if not already set

## Description

There was a bug in the `from_visium` ingestion where ingestion would fail if no `SOMAContext` was provided and no default `SOMAContext` was set.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d0b669e8b829`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.