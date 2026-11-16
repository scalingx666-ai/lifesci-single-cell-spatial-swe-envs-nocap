# Issue

**Title:** Add cavity continuity QC to section ordering

## Description

## Summary

- include internal-cavity topology in every anchored morphology proposal
- report graded cavity blocks with single-section gap tolerance
- bind cavity measurements to proposal fingerprints and approval
- expose the continuity summary API and document the review contract

## Why

Serial sections with substantial internal missing regions should remain morphologically adjacent. A binary per-slide threshold was too brittle for borderline openings, so the review metadata now uses strong cavity seeds, weaker neighboring extensions, and a one-section bridge while retaining human approval as the final gate.

## Validation

- `ruff check .`
- `pytest -q` (212 passed)
- regenerated the 33-slide validation cohort from frozen approved masks; the v3 proposal exactly matched the approved sequence and reported one cavity block
- audited all seven cohorts in the persistent viewer; each had zero or one graded cavity block

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `644f6e1a5c72`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.