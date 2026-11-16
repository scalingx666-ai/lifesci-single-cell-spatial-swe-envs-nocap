# Issue

**Title:** feat: add configurable columns to PAGA plots

## Description

## Summary

- Add an ncols parameter to sc.pl.paga for wrapping multiple color panels into a grid.
- Preserve the existing single-row layout when ncols=None.
- Keep colorbars aligned with grid panels and validate invalid column counts.
- Add regression coverage and a release-note fragment.

## Tests

- pytest -q tests/plotting/legacy/test_paga.py -k paga_ncols -o filterwarnings=: 8 passed
- Ruff, Python byte-compilation, and git diff --check pass.
- The rest of test_paga.py passes 24 tests; one unrelated test needs to download the existing pbmc3k fixture, which is blocked in this environment.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `08d5a01ef80d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.