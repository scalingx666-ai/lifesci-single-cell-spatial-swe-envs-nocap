# Issue

**Title:** [2/4] Add calculate_image_features with skimage + squidpy-native features

## Description

PR 2/4 of the #982 split (plan: PR-1 tests, PR-2 skimage+squidpy features, PR-3 alignment, PR-4 cp_measure).

Introduces `squidpy.experimental.im.calculate_image_features` for per-cell feature extraction from segmentation masks. This is the foundation that PR-3 (alignment) and PR-4 (cp_measure) build on; **cp_measure integration itself lands in PR-4** so the new hard-dependency conversation (`cp-measure`, `centrosome`) is isolated.

## What's in

- skimage `regionprops` features (`skimage:label`, `skimage:label+image`, fine-grained per-property).
- squidpy-native features: `squidpy:summary`, `squidpy:texture` (GLCM), `squidpy:color_hist`.
- Orchestration: `DropReport`, validation, lazy `_prepare_lazy`, centroid computation, parallel tile dispatch via `joblib`.
- Public function `calculate_image_features(sdata, image_key, labels_key=None, shapes_key=None, features=..., align_mode="strict", ...)`.

## What's deferred to follow-up PRs

- **`cpmeasure:*` feature flags** (PR-4). Flag names are recognised here and raise `NotImplementedError` pointing to the follow-up, not "unknown feature".
- **`align_mode="rasterize"`** (PR-3). Raises `NotImplementedError`. PR-2 supports only `align_mode="strict"` (image and labels must share the same pixel grid).
- **`_classify_dropped_cells`** (per-cell drop-reason diagnostic). Deferred; `DropReport` still tracks `empty_tiles`.
- **`features=None`** now raises. The cp_measure-as-default behaviour lands with PR-4.

## No new hard dependencies

PR-2 adds zero new `pyproject.toml` deps. `cp-measure` and `centrosome` land with PR-4.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c8f8b0ad3ad1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.