# Issue

**Title:** fix(bulk): validate pyDEG input columns

## Description

## Problem

`pyDEG.deg_analysis()` accepted duplicate, overlapping, or missing count-matrix columns and described a simple group-length check as biological-replicate validation. Because `pyDEG` receives only a gene-by-column count matrix and no donor/sample metadata, it cannot determine whether those columns are independent biological replicates.

## Changes

- Require at least two distinct input columns in each comparison group.
- Reject duplicate columns within a group, overlap between groups, missing columns, and non-unique count-matrix columns before importing statistical backends.
- Clarify that column validation does not establish biological replication and direct single-cell users to aggregate raw counts with `ov.single.pseudobulk` first.
- Keep `matplotlib-venn` in the test extra and isolate plotting smoke tests from global matplotlib state so the Python matrix exercises the intended plotting contracts.

## Scope

This PR intentionally does not close #879. Preventing cell barcodes from being treated as biological replicates requires donor/sample metadata or a documented pseudobulk-to-`pyDEG` workflow; that information cannot be inferred from the current `pyDEG` count-matrix interface.

## Local validation

- `pytest -q tests/bulk/test_deg_backends.py -k 'too_few or invalid_group or missing_group or duplicate_count'` — 10 passed
- focused public plotting smoke tests — 3 passed
- `pytest -q tests/pl/test_venn.py tests/pl/test_declutter.py tests/pl/test_panelflow.py` — 59 passed
- Python syntax/flake8 fatal checks and `git diff --check` passed

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e78930e5f059`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.