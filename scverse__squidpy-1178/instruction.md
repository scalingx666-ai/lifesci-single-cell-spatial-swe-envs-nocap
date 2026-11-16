# Issue

**Title:** Stain normalization: foundations

## Description

## Summary

Substrate for a new histopathology stain-normalization module. Targets Squidpy 2.0. **No public API surface** in this PR — every new symbol lives under the private `squidpy.experimental.im._stain` namespace and there are no re-exports.

What ships:

- **`_constants.py`** — Ruifrok H/E/DAB canonical stain vectors (derived from `skimage.color.rgb_from_hed`), Ruderman RGB <-> LMS <-> Lab matrices, HistomicsTK-compatible SDA scale. Nothing else; no shared "default background", no luminosity threshold, no schema version.
- **`_conversion.py`** — `rgb_to_sda` / `sda_to_rgb` and `rgb_to_lab_ruderman` / `lab_ruderman_to_rgb` on `xr.DataArray`. Each public function compiles to a single fused `apply_ufunc` per chunk; numpy- and dask-backed inputs both stay on the same code path; dask-backed inputs stay lazy end-to-end. `background_intensity` is a required `np.ndarray` of shape `(3,)` — there is no library-wide default because no scanner produces a pure-white background.
- **`_reference.py`** — minimal frozen `StainReference` dataclass holding either a `(3, 3)` stain matrix (Macenko/Vahadane, ships in PR 3) or `mu` / `sigma` Ruderman Lab channel statistics (Reinhard, ships in PR 2). `background_intensity` is required for decomposition methods and forbidden for Reinhard (Reinhard's color transfer is in Ruderman Lab and doesn't model absorbance). Cross-field validation only; no persistence, no cohort fields, no provenance metadata.

Deliberately deferred to the PRs that actually consume them:

- JSON `save` / `load`, schema versioning, `fit_metadata`, `cohort_members`, `per_image_stats`, `max_concentrations` — none have a producer in PR 1. Adding them now would version artifacts we have not shipped.
- `_validation.py` (canonical reorder, third-column completion, `StainFittingError`, stain-matrix angle/rank checks) — purely supports the Macenko/Vahadane fit path, lands with it in PR 3.
- A `DEFAULT_BACKGROUND_INTENSITY` constant or default kwarg — pure-white `[255, 255, 255]` is wrong for every real scanner. PR 3 ships `estimate_background_intensity`; until then callers must pass an estimate or, knowingly, an explicit `np.array([255., 255., 255.])`.

Design decisions:

- Lives under `experimental/im/` alongside the existing SpatialData-native modules (`_detect_tissue`, `_qc_image`, `_make_tiles`, `_feature`). The eventual `experimental/im -> im` promotion is a separate v2.0 effort.
- Conversion primitives are `xr.DataArray`-native from the start, not numpy-only, so PR 2's lazy apply path reuses them unchanged.
- SDA uses `(rgb + 1) / (I_0 + 1)` so that pixels at the supplied white point map exactly to zero. Documented in `rgb_to_sda` docstring.
- No bespoke I/O. Image data is reached through `sdata.images[key]` (starting in PR 2 via the existing `experimental/im/_utils.py::get_element_data` helper); this module never adds a loader.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3a825ff2e090`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.