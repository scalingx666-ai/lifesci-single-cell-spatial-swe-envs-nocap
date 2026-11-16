# Issue

**Title:** Remove log advise heuristic in `preprocessing/utils.py::filter_and_normalize`

## Description

Removes heuristic to determine if `adata.X` should be logarithmized or not.

## Changes
<!-- Please remove section if this PR does change an existing feature -->

* Removes heuristic to advise to logarithmize data or not

## Related issues
<!-- Please list related issues. If none exist, open one and reference it here. -->

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a453d0f6ec21`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.