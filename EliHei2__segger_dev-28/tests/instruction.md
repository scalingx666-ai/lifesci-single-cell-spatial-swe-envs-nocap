# Issue

**Title:** Skip saving a tile if there are no transcript-transcript edges, and save tile in test set if there are no transcript-nucleus edges

## Description

Empty edge_index tensors caused an error raised by `RandomLinkSplit` [here](https://github.com/EliHei2/segger_dev/blob/main/src/segger/data/parquet/sample.py#L1213). Now it's fixed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e83bebfc3041`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.