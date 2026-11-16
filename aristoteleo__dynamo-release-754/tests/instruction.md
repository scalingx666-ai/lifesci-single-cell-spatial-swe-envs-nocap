# Issue

**Title:** Fix matplotlib 3D vector plots (cell_wise_vectors_3d)

## Description

## Summary
`dyn.pl.cell_wise_vectors_3d(..., plot_method="matplotlib")` was broken for the common single-panel case:
1. `TypeError: Axes.scatter() got multiple values for argument 's'`, then
2. `TypeError: Axes3D.text() missing 1 required positional argument: 'z'`.

## Root cause (both in `scatters_single_input`)
- When `ax is None`, the axes was created via `plt.subplots()` (always 2d), **ignoring `projection="3d"`**. The downstream 3d scatter `ax.scatter(x, y, z, s=..., ...)` then received a *2d* axes, so the `z` column was consumed as the positional `s`, colliding with the keyword `s`.
- Arrowed spines (`add_arrow`) call 2d `ax.text(x, y, s=...)`, which is invalid on a 3d axes.

## Fix
- Create a 3d axes (`figure.add_subplot(111, projection="3d")`) when `projection == "3d"`.
- Skip arrowed spines when `projection == "3d"` (they are a 2d concept).

Both changes are guarded by `projection == "3d"`, so 2d plotting is unchanged.

## Validation
- `tests/test_pl.py::test_cell_wise_vectors_3d_matplotlib` (new) passes.
- Verified end-to-end on pancreatic endocrinogenesis (3-component UMAP + projected velocity): the 3d quiver now renders.
- 2d `dyn.pl.scatters` / `umap` confirmed unaffected.

This revives the matplotlib path of the 3D-visualization feature originally proposed in #260.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01AD7gAdxa3Zt5uiQVDoANa5

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2ecc0ccfe893`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.