# Issue

**Title:** Python module version export fixes

## Description

This PR fixes the version exporting of the `leidenalg` Python module, but more work is needed for the `SpatialDE` module. The change for `leidenalg` was simply to go from `leidenalg.__version__` to `leidenalg.version`, but no such simple change works for `SpatialDE`. Installing `setuptools` and various other possible solutions from Google did not work either.

## PR checklist

- [X] This comment contains a description of changes (with reason).
- [X] Make sure your code lints (`nf-core lint`).
- [X] Fix `SpatialDE` version export.
- [X] `CHANGELOG.md` is updated.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3fc94d7795f1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.