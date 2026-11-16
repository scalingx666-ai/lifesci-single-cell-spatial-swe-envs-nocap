# Issue

**Title:** refactor: share trend fitting and remove redundant PreTSA backend

## Description

## Summary
- Delegate RunDynamicFeatures() numerical fitting to thisutils::fit_trends().
- Remove duplicated PreTSA R/C++ fitters and redundant backend tests.
- Remove the unused pretsa_backend argument; explicit callers must omit it.
- Preserve the public function name, other effective parameters and stored result fields.
- Update documentation, focused tests and styler formatting.

## Validation
- 17 focused assertions passed locally on macOS.
- GAM and PreTSA complete stored outputs were identical before/after backend-argument removal.
- Earlier isolated installation passed; final source tests passed after formatting.
- No claim of hosted CI or Windows validation.

## Dependency
Requires the companion thisutils shared-trend-fitting PR to be merged and installed first. No new inferCSN dependency or dependency version floors.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7914fb263691`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.