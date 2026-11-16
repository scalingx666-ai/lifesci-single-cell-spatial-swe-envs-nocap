# Issue

**Title:** Never clip values by 0.99 quantile in raw readers

## Description

In some readers, raw values were clipped to the 99th percentile. We remove this bad-practice behavior to keep the original values.

This concerned:
- `sopa.io.hyperion`
- `sopa.io.bioio` ONLY when the original dtype is float (which should be extremely rare).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7499ea1146b1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.