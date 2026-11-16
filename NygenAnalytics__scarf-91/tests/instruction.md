# Issue

**Title:** Feature/harmony

## Description

## Change log
Added capability of batch correction through Harmony using https://github.com/slowkow/harmonypy package.

## Known caveats:
The current harmony implementation requires the whole dimension reduced matrix to be stored in memory. This may effect Scarf's capability to scale to large datasets when using Harmony.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `87c8bae986e3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.