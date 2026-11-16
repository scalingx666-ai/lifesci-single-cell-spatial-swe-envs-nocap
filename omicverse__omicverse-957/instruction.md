# Issue

**Title:** feat(pl): add optional trend guides to cellproportion

## Description

## Summary

- add an opt-in `trend=True` mode to `ov.pl.cellproportion`
- connect cumulative stacked proportions in the explicit `groupby_li` order
- support vertical and transposed plots plus `trend_kwargs` styling
- keep the existing output unchanged by default

The connecting lines are documented as visual guides across ordered discrete groups, not fitted statistical trends.

## Validation

- `python -m pytest tests/pl/test_cellproportion_trend.py tests/pl/test_generic_plots.py -q` (`139 passed`)
- `python -m pytest tests/pl/test_cellproportion_trend.py tests/pl/test_ax_contract.py tests/architecture/test_pl_canonical_aliases.py::test_plot_cellproportion_warns_and_delegates -q` (`26 passed`)
- visual smoke test for stacked bars plus cumulative boundaries
- `git diff --check`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c30f9a6ef7a9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.