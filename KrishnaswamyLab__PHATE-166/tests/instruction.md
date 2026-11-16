# Issue

**Title:** Add disconnection warning

## Description

Renames `_graphtools_supports_random_landmarking` to `_graphtools_version_is_at_least_2_0` for improved clarity and forward compatibility. This change enables graceful error handling when working with older versions of `graphtools`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e92046953222`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.