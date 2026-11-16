# Issue

**Title:** Fix dendrogram crashes, simplify Deformation, and let group heights be compared

## Description

Two things prompted this: the dendrogram computing path was hard to follow, and grouped dendrograms with a meta tree often look unbalanced — dense at the bottom, sparse and disproportionately tall at the top.

Profiling first, because it changes what "efficiency" means here. On an 800×200 heatmap with 2 dendrograms and 7 side plots, `_deform` is **0.5%** of render time and `dendrogram.py` **0.6%**; matplotlib artist construction is 96.8%. `Deformation` is not a hotspot and this PR claims no speedup. `_compute_linkage` is the only real algorithmic cost and it is already memoized once per axis with a fastcluster path.

What profiling did turn up was four crashes.

## Crashes fixed

All four reproduce on `main` today:

| Repro | Failure |
|---|---|
| `Heatmap([[0,0,0],[0,0,0],[0,0,0],[1,1,1]]).add_dendrogram("left").render()` | `ValueError: Axis limits cannot be NaN or Inf` — the min-max interval is zero when a block of rows is identical |
| `Dendrogram(rng.random((2500, 10)))` | `RecursionError` — scipy recurses once per tree level and single linkage chains, so the default limit runs out at ~2500 leaves. Measured depth is ~0.65 frames per leaf |
| `GroupDendrogram` over two groups with the same centroid, then `.draw()` | `KeyError` — leaf positions were found by masking for zero height, but a zero-height *merge* is not a leaf |
| `group_rows` producing a one-row group, then `get_row_linkage()` | `AttributeError: no attribute 'Z'` — the singleton branch never set it |

The leaf positions now come from the structure (scipy places leaf *i* at `icoord` `5 + 10i`) rather than from a value mask. With a correct skeleton the 25-line hand-rolled piecewise-linear x-remap underneath is exactly `np.interp`, verified identical to 1e-11.

Three smaller ones in the same path: an ndarray of per-gap spacings silently degraded to the scalar branch (`np.ndarray` is not a `typing.Sequence`) and overcounted the total; spacing summing past 1 divided by zero instead of raising the way `layout._split` does; the divider line mixed model x at one end with render x at the other.

## Deformation

Every operation was a permutation followed by slicing at chunk offsets, but grouping, splitting, the leaf order inside each chunk and the order of the chunks were applied as four separate passes over progressively more nested lists. Hence `reorder_by_col` needing four levels of `ndim` branching plus a `split="2d"/"1d"` flag, and the reorder pass mutating the caller's list in place.

They compose. Resolving them once into a flat index plus chunk bounds makes deforming anything a take along the last axis followed by slices. `transform_row` and `transform_col` become the same function — `transform_row` was already transposing in and out, which is what `axis=-1` means.

Also: state moved off class attributes (including two mutable dicts, with no `__init__` at all) into one object per axis, and the ten `row_*`/`col_*` method pairs collapsed onto single axis-parameterized implementations behind the same public names.

`set_row_chunk_order`/`set_col_chunk_order` are fixed as a side effect — the ratios honoured the chunk order but the data pass returned early unless clustering was on, so the axis widths moved and the data did not.

`split_by_row`, `split_by_col`, `split_cross`, `reorder_by_row` and `reorder_by_col` were never meant to be public but autodoc published them, so they stay as deprecated shims for one minor.

## Visual balance

The cause is measurable. Merge heights were min-max stretched into `[0.2, 1.2]` **in the constructor, per dendrogram, overwriting the values scipy computed**. Every group therefore drew exactly as tall as every other one: on one fixture a group whose rows merge at 0.06 and a group that merges at 9.51 both reached the same apex, so a tight cluster looked as deep as a diffuse one and the meta dendrogram sat on a flat plateau of equal-length stubs.

Keeping the raw heights and moving the scaling to whoever owns the drawing is what makes a scale shared *across* groups possible at all. Two orthogonal knobs on `add_dendrogram`:

- `height_scale` — `"minmax"` (unchanged default) | `"group"` | `"shared"`. `"shared"` measures every group against the tallest merge anywhere, so the drawn apex ratio equals the real distance ratio and a tight group finally draws short.
- `height_transform` — `None` | `"sqrt"` | `"log"` | `"rank"` | callable. For bottom-heavy trees, where merges bunch up near the leaves and leave the top empty. On 60 rows with `method="ward"`, the fraction of merges below half height goes 0.85 → 0.47 under `sqrt`, and to 0.5 by construction under `rank`. Opt-in, because it makes the default `single` linkage *worse* and trades away readable distances. No transform may reorder two merges; that is asserted.

Under a real scale `meta_ratio` also becomes exact. It was off by 8/7, because the meta carried the same 0.2 floor as the bases and its normalization was commented out. The dead band of parallel stubs between the base apexes and the meta's first merge drops from 10.2% of the axis to whatever the groups' actual similarity justifies.

## Compatibility

The default stays `"minmax"`, so this is opt-in and no shipped figure moves. Nine rendered configurations — grouped, cut, cross-split, meta-only, base-only, with side plots, singleton group — are **pixel-identical to `main`**.

Two API notes for the changelog: `Dendrogram.y_coords` is now scipy's raw `dcoord` rather than pre-normalized (use `_render_y_coords` for drawn coordinates, or the new `max_height`), and `GroupDendrogram.divider`/`den_ylim` are filled in by `draw()` rather than `__init__`, since they depend on the scale asked for.

## Verification

The existing deform tests only asserted that no elements were lost, so they passed just as happily when rows came out in the wrong order. The first commit adds the safety net before anything else moves:

- the exact row and column permutation for all 16 cluster/split combinations under both `cut_*` and `group_*` splitting
- the main canvas and the side plots agreeing on that order — untested before, and the whole point of the module
- ratios matching chunk sizes, transform idempotence, no input mutation, clustering running exactly once, no shared class state, `deepcopy` independence
- `GroupDendrogram.draw()` geometry, which had no coverage at all, plus the x-interpolation and slot-containment invariants that keep the dendrogram aligned with its heatmap chunks
- the four crashes as `xfail(strict)`, each flipped by the commit that fixes it

509 tests pass. Every shipped example that draws a dendrogram still runs.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5e1ac6db8495`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.