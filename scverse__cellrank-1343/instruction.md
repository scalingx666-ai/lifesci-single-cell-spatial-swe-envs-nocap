# Issue

**Title:** ci(test): upload rendered plotting figures as an artifact

## Description

Foundation for the ongoing plotting-test refactor (#1328): make ground-truth figure regeneration **platform-correct and painless**, so subsequent class migrations can pin a tight tolerance without baseline drift.

## The problem this solves

Pixel baselines must be produced by the same renderer CI validates against (Linux). A figure regenerated on a maintainer's macOS machine drifts and fails CI at a tight tolerance — which is exactly what blocks tightening `STRICT_TOL` on the drift-prone classes. Today nothing exposes the Linux-rendered PNGs, so there's no way to obtain a correct baseline.

## What this does

- Adds an `upload-artifact` step to the `Test` workflow that publishes `tests/figures/*` (where the plotting tests already render) as the **`rendered-figures`** artifact.
- Uploaded from the **Linux `hatch-test.py3.12-stable` job only** — the canonical baseline renderer. Not macOS, not pre-release, not PETSc (we only ever need Linux baselines; also avoids artifact-name collisions and 4× duplication).
- `if: always()` so figures are available even when an image comparison fails (the actual is saved before the assertion) and from passing runs (needed when intentionally tightening tol).
- Bounded: `retention-days: 14`, `compression-level: 0` (PNGs are pre-compressed).
- Documents the regeneration loop + the three plotting-test flavours (visual / introspection / smoke) in `contributing.md`.

## Why this still catches regressions

CI never updates baselines on its own. Every run compares freshly-rendered output against the **committed** figures and fails on drift — that's the regression gate. This PR only makes CI *expose* what it rendered. Promoting an artifact figure to a baseline is a deliberate, human-reviewed commit (like updating a test snapshot). Same model as squidpy / spatialdata-plot.

## Storage footprint

- One run today: ~203 PNGs, **~5–6 MB** (DPI=40; avg ~22 KB each). Shrinks to ~1–2 MB as the refactor reduces image tests.
- Single uploading job + `retention-days: 14` → peak ≈ size × runs-in-window, self-expiring (~tens to low-hundreds of MB, decaying). Public repo; squidpy and spatialdata-plot run the same `always()` upload with **no** retention cap and no issue — this is strictly more conservative.

## Regeneration loop (now documented)

push → CI renders on Linux → download the `rendered-figures` artifact from the `py3.12-stable` job → review the changed figures → copy into `tests/_ground_truth_figures/` → commit → CI validates against the updated, Linux-matching baselines.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `67e8f4212847`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.