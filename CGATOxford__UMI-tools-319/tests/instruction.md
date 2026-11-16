# Issue

**Title:** Refactored UMIClusterer to remove unncessesary arguement to __call__

## Description

Call signature for `UMIClusterer` was `__call__(umis, counts, threshold=1)`  where `umis` was a list of UMIs and `counts` was a dictionary mapping UMIs to their counts. This seemed unnecesssary as `umis` could be recovered from `counts` with `counts.keys()`. When I wrote the API website page, I pretended it wasn't there. This pull makes the reality match the docs.

Also fixes pysam<0.14 errors if tag is missing.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e1be5a2e7059`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.