# Issue

**Title:** [python] Update Carrara tests to use new SOMAContext

## Description

The Carrara tests were still using the newly deprecated `SOMATileDBContext`. Update to use `SOMAContext` class instead. While making this change, also switch to use `tiledb.client.assets.delete_asset` instead of `tiledb.Array.delete_array` to delete arrays.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `28967a5484e3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.