# Issue

**Title:** bugfix: removes caching from dataset.map function

## Description

HuggingFace tokenized data uses only `keep_in_memory` parameter for toggling memory/caching. Adding a `cache_file_name` results in an error where outdated fields (keys) are used when saving the dataset to disk.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a7953698eac6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.