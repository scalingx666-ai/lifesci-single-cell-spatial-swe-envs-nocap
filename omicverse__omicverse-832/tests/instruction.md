# Issue

**Title:** fix(flowsig): support squidpy imports without pkg_resources

## Description

## Summary

- Install a narrow `pkg_resources` compatibility shim immediately before FlowSig imports `squidpy` for spatial preprocessing.
- Add a regression test that simulates the `squidpy` import path when `pkg_resources` is absent under newer setuptools versions.

## Root cause

Setuptools 82 no longer provides `pkg_resources`, but optional spatial dependencies reached through the FlowSig `squidpy` path can still assume the module exists. This caused FlowSig spatial preprocessing to fail before running the actual Moran's I workflow.

## Validation

- `git diff --cached --check`
- `/Users/mx/Study/repositories/omicverse-develop/.venv/bin/python -m pytest tests/external/test_flowsig_pkg_resources_compat.py -q`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `812bcdf12b57`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.