# Issue

**Title:** fix: downsample_counts(total_counts=...) silently did nothing for Fortran-ordered dense X

## Description

- [x]
- [x] [Tests][] included or not required because: added `test_downsample_total_counts_fortran_order`, red on `main`, green with the fix
- [ ] [Release notes][] not necessary because: release note `docs/release-notes/4408.fix.md` is included

### Pain

`sc.pp.downsample_counts(adata, total_counts=...)` with a dense `X` that is Fortran-ordered returns silently and leaves the data completely unchanged. No error, no warning: a pipeline that asks for 1000 total counts keeps all 7505 and every downstream result is quietly wrong. From the linked issue:

```
C-order 7505.0 -> 1000.0
F-order 7505.0 -> 7505.0
```

### Root cause

`_downsample_total_counts` in `src/scanpy/preprocessing/_simple.py` flattens dense input with `v = x.data if isinstance(x, CSBase) else x.reshape(-1)` (line 949 on `main`), then downsamples `v` in place and returns `spc.x` on the assumption that `v` aliases `x` (the invariant stated in the adjacent comment). That assumption only holds for C-contiguous input: `reshape(-1)` must iterate in C order, so for an F-contiguous array numpy cannot return a view and silently returns a copy. The numba kernel then zeroes and refills the copy, and the untouched original is returned. The same discarded-copy pattern has been there since the dense path was introduced in commit 33b70901 (PR #474) as `X.view().reshape(...)`, and was carried through the refactor in 9de11b14 (PR #3983). The `counts_per_cell` path is not affected because `rows[rowidx]` is a basic slice that writes through in any memory order, which is also why the C-order test suite never caught it.

### The fix

Two lines in `_downsample_total_counts`: after the in-place downsample, if `v` does not share memory with `x` (dense only, sparse `.data` always aliases), write the downsampled flat result back into the original layout:

```python
if isinstance(x, np.ndarray) and not np.shares_memory(v, x):
    x[...] = v.reshape(x.shape)
```

This keeps C-order behavior byte-for-byte identical (no extra work when `v` is a view), preserves the input memory order, and makes F-order results exactly equal to C-order results for the same rng seed.

### Test

`test_downsample_total_counts_fortran_order` in `tests/test_preprocessing.py`: runs the same downsample on `np.ascontiguousarray` and `np.asfortranarray` copies, asserts the F-order sum is actually reduced to the target, asserts elementwise equality with the C-order result, and asserts the input stays F-contiguous.

Before (on `main`):

```
C-order 7505.0 -> 1000.0
F-order 7505.0 -> 7505.0
```

After:

```
C-order 7505.0 -> 1000.0
F-order 7505.0 -> 1000.0
```

The new test fails on `main` (`assert np.float32(7505.0) == 1000`) and passes with the fix; `pytest tests/test_preprocessing.py` is otherwise green.

### How this was found

This fix was located with Vestiges Causal Walk (https://github.com/samvallad33/vestige): the failure was recorded as a symptom memory, a backward causal walk over recorded edges ranked the mechanism (the order-dependent `reshape` view/copy switch), the unverified aliasing contract, and the origin commit, and the ranked causes were verified against a local repro before writing any code.

[tests]: https://scanpy.readthedocs.io/page/dev/testing.html#writing-tests
[release notes]: https://scanpy.readthedocs.io/page/dev/documentation.html#adding-to-the-docs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b92a4dee9ad9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.