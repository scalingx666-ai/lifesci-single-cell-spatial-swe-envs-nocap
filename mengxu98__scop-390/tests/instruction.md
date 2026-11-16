# Issue

**Title:** fix: reject Windows Python execution aliases

## Description

## Summary
- reject the Microsoft WindowsApps `python3.exe` execution alias before launching the cell2location subprocess
- direct users to the configured SCOP conda environment when the resolved path is not executable
- make mocked cell2location tests independent of the host's `python3` app alias

## Validation
- `test-cell2location.R`: passed
- `pkgload::load_all('.', quiet = TRUE, compile = FALSE)`: passed
- `git diff --check`: passed
- prescribed local `rcmdcheck`: 0 errors, 2 inherited warnings, 4 inherited notes; unstated example dependencies check passed. The warnings are unchanged main-branch dependency/Rd issues outside this two-file diff.

This does not change cell2location model parameters or scientific output parsing.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `06a934438d9b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.