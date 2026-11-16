# Issue

**Title:** fix: reproducible niche Leiden clustering + expose flavor/random_state/n_iterations

## Description

Fixes the squidpy integration-CI failures in `tests/graph/test_niche.py` (scverse/squidpy#1260).

Two root causes:
- `calculate_niche_neighborhood`/`_utag` silently dropped `random_state`/`n_iterations` on the Leiden path and used the deprecated `leidenalg` backend, so niche labels were unseeded and unstable across `leidenalg`/`igraph` versions (the `assert np.False_` failure).
- The `spatialleiden` tests hard-failed with `ImportError` when the optional dep was absent.

Changes:
- Expose `flavor` (default `"igraph"`), `n_iterations` (default `-1`), `random_state` (default `0`) on `calculate_niche_neighborhood`/`calculate_niche_utag`; thread them through `_LeidenClusterer` and the deprecated `calculate_niche` umbrella (where they were previously marked "unused").
- Default the Leiden backend to `igraph` with a fixed seed -> reproducible labels. **Changes default niche labels** vs earlier releases.
- Guard the two `spatialleiden` tests with `importorskip`; regenerate the pinned exact labels for the nhood/utag/library/multipostprocessor tests.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `82af8ea44dac`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.