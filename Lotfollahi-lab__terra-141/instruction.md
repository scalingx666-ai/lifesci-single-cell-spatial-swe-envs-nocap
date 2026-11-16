# Issue

**Title:** Add in-silico perturbation scoring to terra.inference

## Description

## Summary
Adds the in-silico gene-perturbation scoring used to quantify knockout effects on TERRA embeddings, at two resolutions:

- **Per-cell** (`token_distance.py`, `infer_token_distance`): Sinkhorn / energy / MMD distance between a cell's unperturbed vs. perturbed *token-embedding clouds* (cell / spatial-cell / neighborhood levels), aligned by `cell_id`. Drives the per-cell tissue mapping.
- **Population / per-label** (`summarize_distance.py`, new): `summarize_{w1,w2,energy,mmd,cosine}_by_label` compute distribution distances between the unperturbed and perturbed *pooled per-cell embeddings*, grouped by a niche/cell-type label. Reuses the single `_geomloss_distance_pointcloud` from `token_distance` (no duplicate implementation).

Also:
- `inference/__init__.py`: export `infer_token_distance` + the `summarize_*` functions.
- `simple_infer_runner.py`: CLI runner for `infer_token_distance`.
- `pyproject.toml`: declare `geomloss` under a new optional `perturb` extra (required by the scoring code but previously undeclared).

## Context
Ports the tissue-mapping work (previously only on the `mapping-gene` branch under the old `src/app` / `nichejepa` layout) into the current `src/terra` layout. Internal imports rewritten `app.utils`→`terra.utils.helper` and `nichejepa.*`→`terra.*`. No overlap with existing `score.py` (`get_spatial_score` / `get_emd_distance` do gene-gene cosine, not perturbation distances).

## Verification
Fresh venv, `pip install -e '.[perturb]'`, then:
- `from terra.inference import infer_token_distance, summarize_w2_by_label, ...` imports cleanly.
- Synthetic-data run of `summarize_w2_by_label` (+ w1/energy/mmd/cosine): one score per group; identical clouds -> ~0.
- `pytest --collect-only` -> 210 tests collect; `tests/test_inference` 7 skipped (opt-in), `tests/test_utils` 16 passed.

Note: `infer_token_distance` end-to-end needs a real model + tokenized dataset (not run here); verified to import and be callable.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6731729f4f81`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.