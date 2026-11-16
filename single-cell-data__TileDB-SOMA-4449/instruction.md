# Issue

**Title:** [python] Document current update obs/var limitation

## Description

**Issue and/or context:** [SOMA-949]

**Changes:** Document that deletion creates gaps in `soma_joinid` values, which currently blocks updates via `update_obs` and `update_var` methods.

**Notes for Reviewer:** Fixes for these limitations are in progress.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1ba587f8a30a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.