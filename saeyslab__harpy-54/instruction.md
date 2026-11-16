# Issue

**Title:** SC_26 custom aggregate multiple

## Description

- custom aggregation of masks and image layers for any callable. 
- support for extraction of multiple features in one map_overlap operation
- add sanity check to output, so code fails if depth/chunks is choosen not big enough

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `308045194db6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.