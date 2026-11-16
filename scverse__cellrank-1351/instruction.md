# Issue

**Title:** feat(estimators): add `which="initial_and_terminal"` to plot_macrostates

## Description

## Description

.

Adds a new aggregate plotting mode `which="initial_and_terminal"` to `TermStatesEstimator.plot_macrostates` that shows both initial and terminal macrostates in a single plot. To tell them apart, legend entries are renamed to `initial: <name>` / `terminal: <name>`.

```python
g.plot_macrostates(which="initial_and_terminal")
```

This is the standard discrete plot (top-N cells per macrostate, outlined over a greyed background), now combining both state sets in one view. It also supports `discrete=False` (continuous memberships), `same_plot=True/False`, and the usual kwargs (`legend_loc`, `basis`, `color`, `mode`, …) since it reuses the existing `_plot_discrete` / `_plot_continuous` rendering paths.

### Example (pancreas + PseudotimeKernel)

Initial state `Ngn3 low EP` and terminal states `Alpha`/`Beta`/`Delta`/`Epsilon` in one UMAP, legend prefixed `initial:` / `terminal:`.

## What changed

- `plot_macrostates`: extended the `which` `Literal` and docstring; added dispatch for the new mode and a readable plot title (`"initial and terminal states"`). The existing `which="all"` title behavior is unchanged.
- New helper `_combine_initial_terminal(discrete)` merges the `_init_states` and `_term_states` holders into a single `StatesHolder`:
  - **discrete**: renames each side's categories, merges the categorical assignments, and concatenates colors in category order;
  - **continuous**: concatenates the two membership `Lineage`s with renamed names + concatenated colors;
  - raises a clear `RuntimeError` if either initial or terminal states haven't been computed.
- In the rare `allow_overlap=True` case where a cell belongs to both an initial and a terminal state, the initial assignment takes precedence in discrete mode (a single categorical can't represent both).

## Tests

Added to `tests/test_gpcca.py`:
- structure of the combined holder (categories, colors, membership names),
- the "compute states first" guard,
- the invalid-`which` error,
- a parametrized smoke test over `discrete × same_plot` for the plotting call.

## Notes for reviewers

- No change to the AnnData serialization contract or to existing `which` modes; this is purely additive.
- `_combine_initial_terminal` only merges representations that exist on both sides (assignments for discrete, memberships for continuous), so estimators that don't compute memberships still work in discrete mode.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7a75885df7f3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.