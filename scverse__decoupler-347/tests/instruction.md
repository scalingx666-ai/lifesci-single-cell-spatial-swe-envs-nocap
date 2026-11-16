# Issue

**Title:** Fix mt.ora selecting the bottom instead of the top n_up features

## Description

.

## The bug

`src/decoupler/mt/_ora.py`:

```python
row = sts.rankdata(row, method="ordinal")   # ascending: rank 1 = smallest value
row = ranks[(row > n_up) | (row < n_bm)]
```

Ranks are **ascending**, so the top features hold the *largest* ranks. `row > n_up` therefore kept `nvar - n_up` features — everything but the bottom `n_up` — rather than the top `n_up`. With the default `n_up` (top 5%), 95% of the features were selected as observed. `decoupler<2` compared against `len(c) - n_up`; the subtraction was lost in the rewrite.

The reported crash follows from that: selecting ~all features makes `a + c` exceed `n_bg`, so `ab + ac > abcd + a` trips the `invalid contingency table` guard in `_mlnTest2t`, which surfaces from `prange` as an opaque `SystemError`. Reproduced with `nvar=1000, n_bg=100`; the reporter's numbers (`ac=23750 = 25000 - 1250`, `abcd=20000 = n_bg`) match exactly.

## Changes

- Compare against `nvar - n_up` so the top `n_up` features are selected.
- `n_bm` selected the bottom `n_bm - 1` features (`row < n_bm`); now `row <= n_bm`. Harmless at the default `n_bm=0`, wrong for any explicit value. `decoupler<2` used `n_bottom + 1` as the threshold.
- Restore the up/bottom overlap validation that `decoupler<2` had, and reject `n_bg < n_up + n_bm` up front. That condition is exact: `a + c` always equals `n_up + n_bm`, so a smaller `n_bg` guarantees a negative `d` regardless of the feature set. It would have caught the report with a message naming the actual problem.
- `mt.query_set` shares the `d = n_bg - a - b - c` subtraction and dies with scipy's `ValueError: All values in 'table' must be nonnegative` when the query set is larger than `n_bg`. It now asserts with a message that names the source and the count. This is a validation gap rather than a correctness bug — the input is user-supplied there — but it is the same sharp edge.
- Fixed the `n_up` docstring: the default is the top 5% of *all* features, not of positive ones.

`mt.aucell` is **not** affected — it ranks `-row`, so its `x <= n_up` correctly takes the top `n_up`.

## Why CI did not catch this

`tests/mt/test_ora.py` reimplemented the buggy convention in its own reference implementation (`row > n_up`), so it agreed with the code under test. Those reference implementations now use the correct convention, plus:

- `test_func_ora_selection` — pins the exact contingency table against a hand-built matrix with known ordering, parametrized over `n_up`, `n_bm`, `n_up == nvar` and a float `n_up`. This distinguishes the correct table from the buggy one rather than just checking the sign.
- `test_func_ora_validate` — the two new guards.
- `test_ora_wide` — the reported crash (`nvar - n_up > n_bg`).
- `test_query_set_n_bg` — the `query_set` guard.

All 8 of these fail on the released code and pass here. Full suite: 242 passed (excluding `tests/op` and `tests/ds`, which need network access).

## Release

Adds a `## 2.2.1` CHANGELOG section and bumps `version` in `pyproject.toml` to match.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d5ca690088c0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.