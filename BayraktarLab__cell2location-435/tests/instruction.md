# Issue

**Title:** Fix pandas Series used as numpy array index

## Description

## Summary
 - `AttributeError: 'Series' object has no attribute 'nonzero'`

Newer pandas versions removed `.nonzero()` from Series objects. When a pandas Series boolean mask is used directly to index numpy/sparse arrays, it fails. The fix is to convert to numpy arrays first.

**Changes across 3 files:**
- `docs/notebooks/tutorial_utils.py`: Add `.values` to `slide.var["SYMBOL"] == genes[j]` comparison
- `cell2location/run_colocation.py`: Add `.values` to `sp_data.obs[...] == s` comparison
- `cell2location/plt/plot_expected_vs_obs.py`: Wrap `data.var_names == gene` in `np.array()`

This supersedes #425 by fixing all similar occurrences in the codebase, not just the one in tutorial_utils.py.

## Test plan
- [x] Pre-commit hooks pass (black, flake8, isort)
- [x] CI tests pass

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2163d39eb179`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.