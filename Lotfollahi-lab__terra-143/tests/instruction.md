# Issue

**Title:** Add in-silico perturbation scoring + tutorials to terra.inference

## Description

## Summary
Adds the in-silico perturbation scoring APIs and two documentation tutorials.

**Code**
- `token_distance.py` — per-cell `infer_token_distance` (Sinkhorn/energy/MMD between unperturbed vs perturbed token clouds)
- `summarize_distance.py` — population-level `summarize_{w1,w2,energy,mmd,cosine}_by_label`
- `perturb_dataset(..., return_perturbation_flags=True)` — opt-in per-perturbation flag columns (default off; no behaviour change)
- `simple_infer_runner.py` CLI; `geomloss` added as a `perturb` extra
- **pyproject: cap `datasets>=2.18,<5`** — datasets 5.x breaks `perturb_dataset` flag columns

**Docs**
- `docs/notebooks/perturbation_tutorial.ipynb`, `docs/notebooks/spatial_mapping_tutorial.ipynb` (registered in `docs/tutorials.md`)
- `docs/conf.py`: credit Mohammad Vali Sanian alongside Sebastian Birk

## Verification
Fresh venv: imports resolve; population functions run on CPU + GPU (H200); perturbation & spatial-mapping tutorials run end-to-end on GPU; `pytest` collects (test_utils pass, opt-in inference tests skip).

## Notes
- Tutorials use a de-identified test kidney section (model from HuggingFace `TERRA-96M`; data via a public link) — confirm data-sharing sign-off before publishing docs.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `155e55234171`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.