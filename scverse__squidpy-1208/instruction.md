# Issue

**Title:** test: cap matplotlib<3.11 to stabilize image-comparison baselines

## Description

matplotlib 3.11.0 (released 2026-06-12) shifts scatter/alpha rasterization past the RMS tolerance, failing `test_plot_spatial_scatter_categorical_alpha` (RMS 51.18 vs tol 50) on the `hatch-test ...-stable` envs. This breaks CI **repo-wide** — `main` and every open PR go red once `uv` resolves 3.11.

Cap `matplotlib<3.11` in the **test dependency-group only**; the runtime dependency stays open, so users and downstream libraries still resolve 3.11. Temporary until the baseline is regenerated against 3.11.

Mirrors scverse/spatialdata-plot#713.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3246a548653e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.