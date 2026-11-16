# Issue

**Title:** Fix perturbation Sankey ribbon scaling

## Description

## Summary

This PR fixes the geometry used by `ov.pl.perturb_sankey`.

The previous implementation used equal-height source bars, but computed destination ribbon heights from raw transition probabilities. That placed the right-side ribbon coordinates on a different vertical scale from the right-side destination bars, so ribbons could extend beyond the target cluster bar in cluster-level perturbation Sankey plots.

The fix computes a single normalized `flow_heights` matrix and uses it consistently across the plot:

- each transition row is scaled by the source bar height
- destination bar heights are derived from the summed incoming flow heights
- source and destination ribbon ends use the same normalized flow height

This keeps source bars, destination bars, and ribbons in one coordinate system, preventing ribbons from overflowing beyond the target bars.

## Changes

- Normalize Sankey flow geometry through `flow_heights = ct * src_sizes[:, None]`
- Use the same flow height for both source and destination ribbon ends
- Add a regression test that checks destination ribbons stay within target bars
- Keep the test fixture generic, with non-biological cluster labels and row-stochastic transition rows

## Validation

- `pytest -q tests/pl/test_perturbation.py`
- `python -m py_compile omicverse/pl/_perturbation.py tests/pl/test_perturbation.py`
- `git diff --check`

A separate review pass also checked that the fix puts the source bars, destination bars, and ribbon endpoints on the same normalized vertical scale.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c4fb9c0ed228`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.