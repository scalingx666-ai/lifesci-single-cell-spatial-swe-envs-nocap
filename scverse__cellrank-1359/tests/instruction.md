# Issue

**Title:** test(plotting): replace bilinear-resize fallback; fix dpi propagation

## Description

.

## Problem

`tests/_helpers.py::resize_images_to_same_sizes` ran before every `compare_images`, **bilinearly resizing the rendered figure to the baseline's pixel size** whenever they differed. A size mismatch is itself a signal that something changed (matplotlib/layout/DPI/backend), and resizing both:
- **masked real regressions** — a genuinely different layout was squashed to match, then passed under the RMS tolerance, and
- **manufactured fake diffs** — interpolation blurs the image before the RMS comparison.

## What changed

### 1. Harness: resize fallback → size tolerance + crop
*(`tests/_helpers.py`, `tests/test_plotting.py`)*

- Remove `resize_images_to_same_sizes`.
- Add `assert_image_sizes_close` — a relative size tolerance (`SIZE_RTOL = 0.1`, the size-axis analogue of `STRICT_TOL`): fail loudly on gross size divergence, absorb sub-pixel `bbox_inches="tight"` rounding drift across platforms / matplotlib versions.
- Add `crop_images_to_common_size` — crop (no interpolation) so `compare_images` gets identical dimensions without blurring. The RMS comparison then runs on real, non-interpolated pixels.

This is consistent with #1328's philosophy (robustness via low DPI + tolerance, not pinning) rather than a strict size equality, which would flag ~17 sub-pixel-jitter tests — including baselines #1328 just regenerated.

### 2. dpi propagation fix
*(`src/cellrank/_utils/_utils.py`, `src/cellrank/estimators/terminal_states/_term_states_estimator.py`)*

Removing the resize exposed that `plot_macrostates` rendered **~2.6× too large**: `_plot_discrete` and the `_plot_continuous` non-same-plot branch popped `dpi` and **discarded** it (the `# handled at figure level` comment was never implemented), so `sc.pl.embedding` rendered at scanpy's default ~100 dpi instead of the requested 40.

`save_fig` now accepts an optional `dpi` forwarded to `fig.savefig`, and both embedding paths pass it through. This restores baseline-matching resolution and recovers `test_final_states` / `test_lin_probs` (which now pass). The new param is backward-compatible — all existing callers behave identically.

## Stale baselines (7 `xfail`)

Removing the resize surfaced 7 committed baselines it had been masking. They are genuinely stale and need regenerating on **Linux CI** (they can't be reliably regenerated on macOS — font metrics shift the `tight` bbox). They're marked `xfail(strict=False)` with reasons so they're **tracked, not masked**, and pass without XPASS errors once regenerated:

- **5 GPCCA macrostate-scatter** (`test_gpcca_meta_states*`, `test_gpcca_final_states`) — scvelo→scanpy content drift (#1302, ~69 RMS). The size half is now fixed by the dpi change; the content half remains.
- **`test_proj_default_ordering`, `test_msc_default`** — later layout/figsize changes.

## Coordination with #1328

These 7 should be regenerated and un-`xfail`ed as part of #1328 (they are the canonical visual-regression tests #1328 keeps, not knob tests it converts). **Ordering matters:** the dpi fix must be in the tree *before* those macrostate-scatter baselines are regenerated, otherwise the oversized renders get baked in and have to be regenerated twice. `strict=False` means there's no race if a regenerated baseline lands before its marker is removed.

## Testing

Local (macOS): `298 passed, 7 xfailed, 0 failed` for `tests/test_plotting.py`; `tests/test_gpcca.py` plotting paths `32 passed`. pre-commit clean.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `191810c74ae7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.