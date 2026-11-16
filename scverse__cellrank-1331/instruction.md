# Issue

**Title:** fix(deps): replace deprecated numpy.core / scipy.ndimage.filters imports

## Description

## Summary

Both `numpy.core` (renamed to the private `numpy._core`) and `scipy.ndimage.filters` are deprecated and scheduled for removal, so these imports will become hard `ImportError`s on a future NumPy/SciPy release. Surfaced while reproducing CI failures in the pre-release-deps environment.

- **`src/cellrank/_utils/_lineage.py`**: replace `from numpy.core.overrides import ARRAY_FUNCTIONS` with the supported public API `numpy.testing.overrides.get_overridable_numpy_array_functions()`. The fallback path is preserved.
- **`src/cellrank/pl/_heatmap.py`**: import `convolve` from `scipy.ndimage` instead of the deprecated `scipy.ndimage.filters`.

## Verification

- Confirmed the public NumPy API resolves (302 overridable functions) and `scipy.ndimage.convolve` imports in the Python 3.14 env.
- Verified `_register_handled_functions()` produces an equivalent handled set (`np.sum` registered, `np.expand_dims` still excluded).
- `tests/test_lineage.py`: 107 passed.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6e09064be1ee`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.