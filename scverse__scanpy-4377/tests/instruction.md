# Issue

**Title:** Backport PR #4329: fix: keep FlyBase gene nan when reading 10x mtx

## Description

Manually created backport PR #4329: fix: keep FlyBase gene nan when reading 10x mtx

On main the reader lives in src/scanpy/io/_read.py; on 1.12.x it is still in src/scanpy/readwrite.py,. This PR is that same change, ported manually

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4183c0cf945e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.