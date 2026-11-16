# Issue

**Title:** Deprecate Python 3.7 support

## Description

## Changes

- Remove `typing_extensions` dependency
- Update `setup.py` to require at least Python 3.8.

## Related issues

<!-- Please list related issues. If none exist, open one and reference it here. -->

Artefacts from #965.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `60e8e167f541`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.