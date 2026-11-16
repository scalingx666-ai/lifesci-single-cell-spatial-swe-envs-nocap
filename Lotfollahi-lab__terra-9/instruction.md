# Issue

**Title:** Bugfix/cell graph tokenizer

## Description

- fixes nonzero medians to nonzero means bug
- adds `keep_in_memory`, caching, and `num_shards` options in tokenization
- parallel tokenization of individual files

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cfa46ef8e823`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.