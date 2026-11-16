# Issue

**Title:** Drop scVelo as hard dependency, add as optional pip extra

## Description

Final step of the scVelo removal: drop scVelo from hard dependencies and make it an optional pip extra for velocity embedding stream/grid plots.

## Changes

### `pyproject.toml`
- Remove `scvelo>=0.3` from `[project] dependencies`
- Add `optional-dependencies.scvelo = ["scvelo>=0.3"]` — used by `TmatProjection.plot()` for `scv.pl.velocity_embedding_stream/grid` (already import-guarded via `_check_module_importable`)
- Keep `scvelo>=0.3` in `[dependency-groups] test` — needed for 5 projection tests

### Source docstrings & comments
- Fix stale `scvelo.pl.scatter` → `scanpy.pl.embedding` ref in `_base_kernel.py` random walk kwargs docstring
- Drop `scvelo compat:` prefix from 4 legend-loc normalization comments (code uses scanpy directly now)
- Remove `scvelo/issues/673` URL comment from `_term_states_estimator.py` (bug is in CellRank's own code)

### Tests
- Move top-level `import scvelo` in `tests/_helpers.py` inside `_create_dummy_adata()` — only used for offline test data regeneration, never at test runtime

## What stays
- Attribution comments ("copied from scvelo", "adapted from scvelo") — kept for credit
- `docs/conf.py` intersphinx mapping for scvelo — projection docstrings still cross-reference it
- `tests/conftest.py` try/except scvelo import — sets figdir for projection tests
- `tests/test_plotting.py` `test_scvelo_*` test names — historical, functional

Closes the scVelo removal plan (`.github/prompts/PLAN_scvelo_removal.md`).
Follows #1301 and #1302.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `75f5c52ae9bf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.