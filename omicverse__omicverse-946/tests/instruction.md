# Issue

**Title:** fix(bulk): accept GDC-prefixed clinical fields

## Description

## Summary

Fix `pyTCGA.survial_init()` for clinical TSV exports whose GDC data-model fields are prefixed by their entity names.

- auto-detect legacy columns and current GDC forms such as `demographic.vital_status`, `demographic.days_to_death`, and `diagnoses.days_to_last_follow_up`
- accept an explicit `clinical_columns` mapping for custom or future schemas, plus a configurable `obs_case_id`
- collapse duplicate clinical rows to one record per case and use the latest reported follow-up/death time
- preserve the existing in-place `survial_init()` API and filter AnnData samples with one aligned operation
- raise actionable errors when required identifiers, status fields, or survival-time fields are unavailable

## Root cause

The implementation hard-coded unprefixed columns including `vital_status` and `days_to_last_follow_up`. GDC exposes clinical properties under demographic, diagnosis, and follow-up entities, so current TSV schemas can use names such as `demographic.vital_status`. The direct lookup therefore raised `KeyError: 'vital_status'` before any survival metadata was attached.

The old row loop also assumed duplicate clinical indices and selected only the first record. The replacement aggregates by `case_submitter_id`, selects death time for deceased cases and last follow-up for living cases, and retains the latest valid value when a case has multiple records.

## Validation

- reproduced #867 on `master` with a GDC-prefixed clinical table
- focused TCGA regression: 4 passed
- bulk plus registry regression: 55 passed, 1 skipped
- `python -m compileall -q omicverse/bulk/_tcga.py`
- `git diff --check`

The skipped bulk test and reported warnings are from existing optional/backend paths and are unrelated to this change.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c30f9a6ef7a9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.