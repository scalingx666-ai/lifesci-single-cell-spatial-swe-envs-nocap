# Issue

**Title:** Fix CellRank-emitted warnings

## Description

Fix warnings emitted by CellRank's own code. Upstream warnings (scvelo, scanpy, pygam) are left for separate upstream PRs.

## Changes

### `_base_model.py` — "No data for colormapping" (44× per full run)
Only pass `cmap`/`vmin`/`vmax` to `ax.scatter()` when the color type is continuous. Previously these were always passed, triggering matplotlib's `UserWarning: No data for colormapping` when `c` was a string or categorical array.

### `_log_odds.py` — seaborn deprecation warnings (~25×)
- Replace deprecated `color="black"` gradient palette with `palette="dark:black"` (seaborn v0.14 removal)
- Replace `color=threshold_color` with `palette=f"dark:{threshold_color}"`
- Truncate per-point continuous palette lists to number of hue levels, fixing "palette list has more values than needed"

### `_gpcca.py` — `ImplicitModificationWarning` in TSI (2×)
Convert DataFrame index to string before creating AnnData in `tsi()`, preventing anndata's `ImplicitModificationWarning: Transforming to str index`.

## Testing

All 295 plotting tests pass, 89 GPCCA tests pass, 130 model tests pass — verified locally.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6f6943a42694`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.