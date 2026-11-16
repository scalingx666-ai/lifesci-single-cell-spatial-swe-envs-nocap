# Issue

**Title:** Change preprocessing order

## Description

This PR moves the unification before the `SCANPY_FILTER` step. This is necessary because we rely on mitochondrial genes having an MT-prefix, which is not the case if only gene IDs are available. With the new order, everything is first converted to symbols.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `79002fca942c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.