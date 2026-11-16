# Issue

**Title:** {ts} count from flatfile

## Description

Resurrects  #125 

This introduces the `count_tab` command to count reads per gene using the flatfile output from e.g FeatureCounts/HTSeq. Currently `count_tab` does not support per-cell counting.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8193b9352f81`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.