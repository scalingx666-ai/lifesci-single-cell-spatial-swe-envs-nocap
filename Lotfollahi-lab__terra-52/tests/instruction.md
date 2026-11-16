# Issue

**Title:** Bugfix/cls graph tokenizer

## Description

Fixes cls for cell graph tokeniser to include `<cls_{i}>` for `i` in range degree of each cell.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1331d5fe2b35`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.