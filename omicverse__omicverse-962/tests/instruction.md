# Issue

**Title:** fix(pl): support count-based CCC heatmaps

## Description

## Summary

- allow `ccc_heatmap(..., display_by="aggregation", value="count")` to use the significant-interaction count matrix
- label count-based color scales as `Number of interactions` instead of `Interaction Strength`
- preserve the CellPhoneDB orientation: row totals are outgoing and column totals are incoming

## Reproduction

Before this change, the aggregation heatmap rejected `value="count"`, while related aggregation views could still label count-valued colors as interaction strength. This made count tables appear inconsistent with the heatmap even though the incoming/outgoing orientation was correct.

## Tests

- added count-measure routing coverage
- added asymmetric incoming/outgoing total coverage
- added count legend coverage for aggregation views
- `pytest tests/pl/test_ccc_plots.py -q` (136 passed)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `23e9dfe2c40f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.