# Issue

**Title:** fix: mesh legend kwargs leak, duplicate layer plotters, and unusable set_legends

## Description

## Problem

**1. `MeshBase._legend_kws` is a class-level mutable default.**

`MeshBase._legend_kws = {}` is a class attribute and `set_legends` mutated it in place with `.update()`. `ColorMesh` and `Colors` rebind it in `__init__` so they are safe; `SizedMesh`, `PatchMesh`, `MarkerMesh` and `TextMesh` never do — so `set_legends()` on any of those four wrote into a dict shared by every `MeshBase` subclass in the process:

```python
a = SizedMesh(d); b = MarkerMesh(d > 0.5)
a._legend_kws is MeshBase._legend_kws   # True
a.set_legends(title='A'); b._legend_kws  # {'title': 'A'}  <- leaked
```

**2. `WhiteBoard.add_layer` never checked or set `_registered`.**

`add_plot` guards with `if plot._registered: raise DuplicatePlotter(plot)`; `add_layer` did neither. A layer plotter carries per-board state — `plot.set(name=...)` at add time, `plan.set_deform(...)` in `ClusterBoard._render_plan` — so the same object added to two boards was silently shared and the second board clobbered the first. `add_layer` also falls back to `plot.name`, so both registrations collided on the same `_legend_switch` / `get_legends` key.

**3. `set_legends` was unusable on `StackBar` and `LayersMesh`.**

Both populate `self._legend_kws` and read it in `get_legends`, but `set_legends` was only overridden on `MeshBase`, so calling it on either hit the `RenderPlan` stub and raised a bare `NotImplementedError`. The options could only be passed through the constructor.

## Fix

- `set_legends` rebinds instead of mutating: `self._legend_kws = {**self._legend_kws, **kwargs}`. No `__init__` needed on the four classes that lack one — the first call creates their instance dict. Every read site is a `**self._legend_kws` unpack inside `get_legends()`, so rebinding is observationally identical for legitimate callers.
- That implementation moves from `MeshBase` up to `RenderPlan`, guarded on `_legend_kws` being present, so `StackBar` and `LayersMesh` get it too. Plotters that take no legend options still raise `NotImplementedError`, now with a message naming the class rather than an empty traceback.
- `add_layer` raises `DuplicatePlotter` as its first statement (before the `_legend_switch[name] = legend` write, matching `add_plot`) and sets `plot._registered = True` before appending to `_layer_plan`.
- Two missing spaces in `DuplicatePlotter.__str__`, which rendered as ``The `X` addedto the `main` has been registered,please create...``. Worth doing now that there is a second raise site.

## Compatibility

Swept `tests/`, `docs/` (including `.. plot::` blocks), `scripts/`, `app/` and library internals (`heatmap.py`, `layers.py`, `oncoprinter/core.py`) — no call site passes one plotter object to `add_layer` twice or to two boards. `_copy_board` does share already-registered layer plotters between composite boards, but it copies `_layer_plan` directly and never calls `add_layer`, so the new guard cannot fire there.

`RenderPlan.set_legends` loses its `*args`; it was never callable with positional arguments (the only implementation, on `MeshBase`, was keyword-only).

## Tests

Five regression tests, each verified to fail on the pre-fix code:

- `test_set_legends_does_not_leak_between_plotters` — two independent mesh plotters do not see each other's legend options, and `MeshBase._legend_kws` stays `{}`.
- `test_duplicate_layer_plotter_raises` — one `ColorMesh` added as a layer to two boards raises `DuplicatePlotter`.
- `test_set_legends_on_stackbar` — `set_legends` merges into the constructor defaults and the board still renders with legends.
- `test_layersmesh_set_legends` — same merge behaviour for `LayersMesh`.
- `test_set_legends_unsupported_raises` — a plotter without `_legend_kws` still raises `NotImplementedError`.

`pytest tests -q`: **524 passed, 6 xfailed** (baseline 519 passed, 6 xfailed).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `13d29687f69b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.