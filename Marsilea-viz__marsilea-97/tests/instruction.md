# Issue

**Title:** fix: reject seaborn plots layered onto a mesh canvas

## Description

, which noted this while fixing the flank-side alignment.

## Problem

Layering a seaborn plotter onto a canvas that already holds a mesh produced a silently broken figure:

```python
h = ma.Heatmap(data)           # ColorMesh on the main canvas
h.add_layer(mp.Strip(obs))     # seaborn plot on the same axes
h.render()
```

The two disagree about what the axes coordinates mean. A mesh draws cells over `0..n` on both axes; a seaborn plot puts categories at `0..n-1` and rescales the other axis to the data values. Whichever renders last wins:

| axis | mesh needs | actual |
|---|---|---|
| x | `(0, 8)` | `(-0.5, 7.5)` — categories half a cell off, 25 px on an 8-column canvas |
| y | `(8, 0)` | `(2.63, -2.66)` — heatmap row axis overwritten by the strip's value range |

No render came out right, and nothing warned.

## Why reject rather than realign

The x offset alone is fixable, but y is not: value space and row space cannot share one axis. A strip plot's values (say -3..3) have no meaning on an axis indexing 8 heatmap rows, so there is no correct figure to fall back on. Making x align would still leave a destroyed heatmap.

So `add_layer` refuses the pairing, next to the existing `render_main` guard, with a message naming both plotters and the supported alternatives:

```
`Strip` and `ColorMesh` cannot share the main canvas. A seaborn plot scales its
axes to the data values, a mesh to the grid of cells, so the categories end up
offset by half a cell and the mesh loses its value axis. Add `Strip` to a side
instead, with `add_top`, `add_bottom`, `add_left` or `add_right`, or give it a
main canvas of its own.
```

## Scope — only the broken pairing is rejected

Verified still working:

- **A seaborn plot owning the main canvas.** This was never misaligned: `0..n-1` lands on the same axis fractions as a side plot's `0..n`. Measured 0.0000 px against a `Colors` side plot.
- **Two seaborn plots layered** — the Violin + Swarm idiom in `scripts/example_figures/violin_swarm.py`. That script still builds its figure end to end.
- **Mesh over mesh** — `Heatmap.add_layer(MarkerMesh(...))`, as used in the pbmc3k gallery example.
- **`Numbers`** — not a seaborn plotter, behaviour unchanged.

The guard fires in both orders (seaborn onto a mesh, mesh onto a seaborn). No docs or gallery example uses the rejected combination.

## Tests

Five tests in `tests/test_board_ops.py`: both rejection orders, plus the three legitimate layerings above — the sole-main-canvas one asserts pixel alignment rather than just that it renders.

Full suite: 517 passed, 6 xfailed. `ruff check` / `ruff format` clean on the changed files.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0b1435ecf4d3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.