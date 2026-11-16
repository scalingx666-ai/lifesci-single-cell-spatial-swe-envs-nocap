# Issue

**Title:** fix(gpcca): clearer error when no macrostate meets stability threshold

## Description

.

## Problem

`GPCCA.predict_terminal_states()` defaults to `method="stability"` with `stability_threshold=0.96`. The method keeps only macrostates whose self-transition probability (the diagonal of `coarse_T`) is `>= stability_threshold`. When *no* macrostate is that stable, the selection is empty and the call forwards `[]` to `set_terminal_states`, which raised the generic, unhelpful:

```
ValueError: No macrostates have been selected.
```

Several users on #1316 hit this and had no way to tell that the real cause was an overly strict default threshold. (`predict_initial_states()` works for them because it uses the coarse stationary distribution rather than a threshold.)

## Fix

Detect the empty selection in the stability branch *before* delegating, and raise an actionable error that reports the threshold, the actual maximum stability, and concrete remedies:

```
No macrostate has a stability `>= 0.96` (maximum stability is `0.7213`), so no
terminal states could be selected. Decrease `stability_threshold`, use a different
`method` (e.g. `'top_n'`), or recompute the macrostates with `.compute_macrostates()`.
```

The generic message in `set_terminal_states` is left intact — it is still correct for the case where a user explicitly passes an empty selection.

## Test

Updated `test_compute_terminal_states_no_selected` to assert the new, more informative message.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `11b6359539d2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.