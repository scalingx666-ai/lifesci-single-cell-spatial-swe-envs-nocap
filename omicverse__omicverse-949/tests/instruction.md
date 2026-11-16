# Issue

**Title:** fix(pp): pass batch labels to DecontX

## Description

. Adds batch_key to remove_ambient / estimate_contamination, validates the obs column, and passes per-cell batch labels to pydecontx.decontx(batch=...). Includes regression tests for backend forwarding and the public API.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c30f9a6ef7a9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.