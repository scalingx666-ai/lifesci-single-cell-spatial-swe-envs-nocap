# Issue

**Title:** feat(airr): custom clone-size bins in clonal_expansion

## Description

.

## What

`ov.airr.clonal_expansion`'s `clip_at` now accepts **either an int (unchanged) or a sequence of bin edges**, so users can define biologically meaningful clone-size intervals instead of getting one category per exact size when looking at large expansions.

```python
# unchanged (backward compatible)
ov.airr.clonal_expansion(adata, clip_at=4)
#  -> '1 (single)', '2', '3', '>= 4'

# NEW: custom bins (upper-inclusive, strictly-increasing positive edges)
ov.airr.clonal_expansion(adata, clip_at=[1, 5, 10, 50, 100])
#  size==1 -> '1 (single)'
#  2..5    -> '2-5'
#  6..10   -> '6-10'
#  11..50  -> '11-50'
#  51..100 -> '51-100'
#  >100    -> '>100'
```

## Details

- **Backward compatible**: an `int` `clip_at` takes the exact existing code path (`'1 (single)','2',…,'>= N'`).
- **Custom bins**: a sequence is interpreted as upper-inclusive edges; consecutive edges form ranges (`2-5`, `6-10`, …), a leading `1` becomes `'1 (single)'`, sizes above the last edge go to `'>{last}'`.
- **Validation**: edges must be positive and strictly increasing (else `ValueError`); empty sequence rejected.
- Result remains an **ordered categorical** in `obs[key_added]`, so `clonal_expansion_plot` renders the custom bins in order with no changes.

## Tests

`tests/airr/test_clonal_expansion.py` (8 tests): int backward-compat, the issue's exact `[1,5,10,50,100]` mapping, non-singleton first edge, invalid-bin `ValueError`s, and the missing-column `KeyError`. All pass locally.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `928df87e50ec`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.