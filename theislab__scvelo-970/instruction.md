# Issue

**Title:** Deprecate Python 3.7

## Description

## Changes

<!-- Please remove section if this PR does change an existing feature -->

- Update `scvelo/__init__.py` to drop support for Python < 3.8.

## Related issues

<!-- Please list related issues. If none exist, open one and reference it here. -->

Artefacts of #965.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `57257276287f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.