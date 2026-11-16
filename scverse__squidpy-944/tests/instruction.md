# Issue

**Title:** Rename `count_file` in internal API to `counts_file`; Improves error message when wrongly specified

## Description

## Description

rename the `count_file` argument in the internal `_read_counts` to match the `counts_file` (with “s”) in the public API.

This changes the error message when it’s wrongly specified from

> TypeError: squidpy.read._utils._read_counts() got multiple values for keyword argument 'count_file'

to

> TypeError: squidpy.read._read.visium() got an unexpected keyword argument 'count_file'. Did you mean 'counts_file'?

## How has this been tested?

CI

## Closes

, but let’s wait for @alexanderchang1 to confirm

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6d13527f7fef`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.