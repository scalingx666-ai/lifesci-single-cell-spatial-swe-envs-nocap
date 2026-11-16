# Issue

**Title:** Add check_sum_tol parameter to compute_fate_probabilities

## Description

## Summary

This PR exposes the validation tolerance for fate probabilities as a separate user-configurable parameter, independent of the solver tolerance.

## Problem

Previously, the validation check that fate probabilities sum to 1 used a hard-coded `rtol=1e-3`. This caused issues when:
- The iterative solver converges successfully but with slightly looser precision
- Users had no way to adjust this tolerance without modifying the source code
- The error message didn't provide enough information to diagnose the issue

## Solution

- Add new `check_sum_tol` parameter (default `1e-3`) to `compute_fate_probabilities()`
- Improve the error message to show the actual range of offending row sums
- This allows users to relax the validation tolerance independently of the solver tolerance

## Example

```python
# Before: no way to fix this without changing tol (which affects solver convergence)
# ValueError: `2040` value(s) do not sum to 1 (rtol=1e-3)...

# After: informative error message
# ValueError: `2040` value(s) do not sum to 1 (check_sum_tol=1e-03). 
# Offending row sums range from 0.997644 to 0.998999. ...

# User can now relax the validation tolerance:
g.compute_fate_probabilities(check_sum_tol=3e-3)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c3478b4576bb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.