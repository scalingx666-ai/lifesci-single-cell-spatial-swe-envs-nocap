# Issue

**Title:** Remove hard `scvi-tools` dependency

## Description

## Changes

<!-- Please remove section if this PR does change an existing feature -->

Make `scvi-tools` install optional as `pip install 'scvelo[vi]'`.

Related to the failing CI, see here: 

## Related issues

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `809632e03acc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.