# Issue

**Title:** Fix lineage-driver correlation scaling

## Description

## Bug fixes

* Correct lineage-driver correlation scaling for dense, sparse, and pairwise-missing inputs.
* Add regression tests comparing all three vectorized paths with `scipy.stats.pearsonr`.

The helpers used population standard deviations but divided the centered cross-product by `n - 1`, inflating correlations by `n / (n - 1)`. The corrected denominator uses the matching observation count while preserving the existing vectorized implementation and missing-value semantics.

This also removes inflated inputs to the downstream Fisher transformation. For pairwise-missing data, lineage-driver rankings may change when the jointly observed sample count differs between gene-lineage pairs.

## Related issues

## Testing

* `uv run pytest tests/test_utils.py tests/test_lineage_drivers.py -q`
* `uv run pre-commit run --all-files`
* `uvx hatch test`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f1f2c06f295d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.