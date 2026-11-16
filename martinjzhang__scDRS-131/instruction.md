# Issue

**Title:** Fix NumPy 2.0 IndexError in Geary's C distribution match

## Description

## Summary

. Under NumPy >= 2.0, `scipy.stats.rankdata(..., method="ordinal")` returns a **float** array, which can no longer be used to index into another array:

```
File ".../scdrs/method.py", line 992, in distribution_match
    return np.sort(ref)[rankdata(v, method="ordinal") - 1]
IndexError: arrays used as indices must be of integer (or boolean) type
```

This casts the ranks to `int` before the `- 1` and the indexing, in two places that share the pattern:

- `scdrs/method.py` — the `distribution_match` helper inside `test_gearysc` (the code path in the traceback).
- `tests/test_method_downstream.py` — the mirrored reference implementation used to validate the same computation, so the test itself runs under NumPy 2.0.

The companion `np.float_` -> `np.float64` change already landed in #106, so this is the remaining fix needed for NumPy 2.0 compatibility.

## Change

```diff
-                return np.sort(ref)[rankdata(v, method="ordinal") - 1]
+                return np.sort(ref)[rankdata(v, method="ordinal").astype(int) - 1]
```

(and the analogous one-line change in the test).

## Testing

With NumPy 2.5.2 / SciPy 1.18.1 in a fresh env, the full suite passes:

```
46 passed
```

In particular `tests/test_method_downstream.py::test_downstream_group_analysis` and `tests/test_CLI.py::test_downstream_cli` (both failing on `master` under NumPy 2.0, per #129) now pass.

Credit to @Jacobog02 who reported #129 and proposed this exact cast.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `638b377bbe90`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.