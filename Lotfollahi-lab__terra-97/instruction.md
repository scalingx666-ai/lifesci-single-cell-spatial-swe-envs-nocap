# Issue

**Title:** Feature/cell masking

## Description

You can control the new masking strategy by either defining the number of targets or supplying a list of segments (targets), where each target represents a full cell (segment) with all its non-zero tokens included.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `793503d907c0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.