# Issue

**Title:** chore(via): remove unused AdjlstGraph import

## Description

## Summary

Removes the unused AdjlstGraph import from VIA random-walk generation.

## Notes

The random-walk implementation continues to use PecanPy through SparseOTF. This cleanup does not remove or change the active PecanPy dependency.

## Validation

- A minimal _rw2_walks() smoke run completed successfully.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3777a62fb8a1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.