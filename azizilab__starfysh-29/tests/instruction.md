# Issue

**Title:** fix: Multi-dimensional indexing error

## Description

Fixes the following ValueError thrown in recent pandas versions: ValueError: Multi-dimensional indexing (e.g. obj[:, None]) is no longer supported. Convert to a numpy array before indexing instead.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fc524ba1e9e6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.