# Issue

**Title:** fix(models): support BaseModel.prepare() with lineage=None when no lineages computed

## Description

## Bug fixes

* `BaseModel.prepare()` is documented to set all weights to :math:`1` when `lineage=None`, but it called `Lineage.from_adata()` unconditionally at the top of the method. On an `AnnData` where no fate probabilities had been computed, this raised `KeyError: "Unable to find lineage data in adata.obsm['lineages_fwd']"` before the documented `lineage is None → weights = 1` branch could ever run.
* Fix: move the lineage lookup inside the `lineage is not None` guard. `probs` is only ever read in that branch, so the unconditional call was both unnecessary and the source of the error. Behavior when a lineage *is* requested (including the invalid-lineage `KeyError`) is unchanged.

## Changes

* Added regression test `TestModel::test_prepare_no_lineage` — deletes the fate-probs `obsm` key, calls `prepare(..., lineage=None)`, and asserts `w_all == 1`. It fails against the old code and passes now.

## Related issues

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4b445f253241`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.