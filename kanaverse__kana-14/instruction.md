# Issue

**Title:** Report the delta detected and log-fold change for each marker.

## Description

This expects a payload that has a `rank_type` property, that is one of:

- `cohen-min/mean/min-rank`
- `auc-min/mean/min-rank`
- `lfc-min/mean/min-rank`
- `delta-d-min/mean/min-rank`

In return, it will return a `lfc` and `delta-d` (the `auc` and `cohen` properties can now be deleted). These are already sorted by the chosen ranking statistic (which is not returned). 

Not 100% sure what to do with the gene names. Perhaps we could transfer them once to the main thread and then only transfer the ordering vector, which should avoid costly string serialization.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `94d46228849b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.