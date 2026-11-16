# Issue

**Title:** ov.tl: species-set prediction (sdm_*) for presence-absence + presence-only data (tbs2/plant)

## Description

TBS RSI branch `tbs2/plant` at 6f9ad1a (plant-distribution-modeling reward 1).

- `ov.tl.sdm_*`: per-survey species-set prediction from presence-absence + presence-only data (spatial hold-out folds, neighbour composition, presence-only histograms, MLP fit + fusion, `sdm_community_pipeline`), sample-F1 decoding of species sets.
- Tests: `tests/tl/test_sdm.py`.

Generic method; no task constants.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `39d7dd521880`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.