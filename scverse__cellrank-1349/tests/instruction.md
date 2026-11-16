# Issue

**Title:** Add `agg` option for fate probabilities towards aggregated terminal states

## Description

## What

Adds an `agg` parameter to `GPCCA.set_terminal_states` and `GPCCA.set_initial_states` controlling how cells are selected when several macrostates are combined into one state via comma-joined names (e.g. `set_terminal_states(states=['A, B', 'C'])`):

- `agg="top_n"` (default) — existing behavior: the `n_cells` most confident cells of the **combined** membership.
- `agg="union"` — the top `n_cells` of **each** constituent macrostate, unioned together, so every macrostate is represented.

.

## Why

As reported in #1000, when aggregating macrostates the previous logic picked the most confident cells of the *combined* membership. If one macrostate dominates, the aggregated state ends up composed almost entirely of that macrostate's cells — it is not representative of the combination, and the resulting fate probabilities inherit the bias.

Verified on the test data with `n_cells=5`: combining two macrostates produced a combined state of only 5 cells (1 from `A`, 0 from `B`) under `top_n`, versus 10 cells (5 from each) under `union`.

## Changes

- `_gpcca.py`: new `StatesAggregation` enum, the `agg` parameter on both setters, and a `_create_aggregated_states` helper that runs cell selection on the individual macrostate columns and relabels them to the aggregated group. Colors/probabilities still derive from the aggregated membership, so the rest of the pipeline is unchanged.
- `_docs.py`: shared `%(agg)s` docstring template.
- `test_gpcca.py`: tests for terminal-state union vs. top_n (incl. fate-probability check), initial-state union, and invalid-`agg` validation.

## Notes for reviewers

- The default (`top_n`) preserves existing behavior, so this is backward compatible.
- `agg` only affects name-based selection; the `dict`/`pd.Series` paths and `predict_terminal_states` are unaffected (their names are never comma-aggregated).
- `pre-commit` (ruff) is clean; the full `TestGPCCA` suite passes locally.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7a75885df7f3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.