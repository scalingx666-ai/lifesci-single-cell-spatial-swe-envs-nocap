# Issue

**Title:** Fix topography_3D PyVista crash when a fixed-point type is absent

## Description

## Problem
`dyn.pl.topography_3D(..., plot_method="pv")` raises:
```
ValueError: Invalid array shape. Empty arrays are not allowed. Array 'colors' cannot have shape (0, 4).
```
whenever the vector field has **no fixed points of some type** (emitting / unstable / absorbing) — which is common.

## Cause
`plot_fixed_points` (pv branch) loops over the three fixed-point-type index groups and builds a `pv.PolyData(Xss[indices])` with `colors[indices]` for each. When a group is empty, the PolyData/colors arrays are empty and pyvista rejects them (and `text_colors[indices[0]]` would also `IndexError`).

## Fix
Skip empty index groups (`if len(indices) == 0: continue`).

## Validation
Verified on pancreatic endocrinogenesis (3D vector field + topography): `topography_3D(plot_method="pv")` now returns a `(Plotter, list)` and `export_html` succeeds.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01AD7gAdxa3Zt5uiQVDoANa5

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `41ef192d8bdc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.