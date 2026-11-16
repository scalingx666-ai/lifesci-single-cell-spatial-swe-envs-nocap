# Issue

**Title:** Improve scanner-edge mask cleanup

## Description

## Summary
- preserve dense central tissue rows while restricting scanner-edge clearing to boundary zones
- recognize thicker connected scanner rails near slide boundaries
- add focused regression tests for both cases

## Validation
- 209 pytest tests passed
- Ruff lint and formatting checks passed
- visually audited preferred KPF cohorts 4352 and 4785 at thumbnail resolution

Generated reviews, source slides, and local operational files are not included.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a2f5a527543f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.