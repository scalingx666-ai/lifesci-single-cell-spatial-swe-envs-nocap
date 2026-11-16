# Issue

**Title:** [c++] Make `ManagedQuery` move constructor 'default'

## Description

The default move constructor has the same behavior as the manually defined one, but is safer if we add additional parameters to the `ManagedQuery`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `63161963b709`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.