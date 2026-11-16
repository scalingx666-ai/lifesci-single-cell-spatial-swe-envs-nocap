# Issue

**Title:** feat(pl): panelflow — a measure-then-place layout engine for exact panels

## Description

`multipanel` is a gridspec: it divides the canvas into cells, and the axes box is whatever is left after matplotlib fits the tick labels. So a column shares one width, a pie chart gets a survival curve's box, and a journal instruction like "panel 45 mm wide" cannot be honoured — 45 mm of *cell* is not 45 mm of *axes*.

`panelflow` inverts the derivation. You declare each panel at its finished **axes** size; decorations are measured from the rendered artists at draw time and reserved *outside* the box. The box stays exactly what you asked for.

```python
fl = ov.pl.panelflow(max_width='nature-double', units='mm', title='Figure 1')
a  = fl.panel('A', 45, 100)              # returns the axes; not made current
ov.pl.violin(df, keys=..., groupby=..., ax=a)
b  = fl.panel('B', 60, 100)              # different width, same row
c  = fl.panel('C', 45, 45, below='A')    # stacks under A in A's column
fl['D'];  fl.savefig('figure1', formats=['pdf', 'svg'])
```

## Why measure instead of guess

A tick label's width is not known until it renders. gridspec handles that by letting the axes shrink; panelflow handles it by reserving measured space and keeping the box fixed. Concretely, same content in both engines:

| | axes box | do the decorations fit? |
|---|---|---|
| gridspec + `panel_size` (#930) | 45×40 mm exact | **no** — long cell-type y-labels overrun the canvas by 541 px at default margins; you have to hand-tune the margin to ~62 mm |
| **panelflow** | 45×40 mm exact | **yes** — the reserve is measured (59 mm here), the box is untouched |

The reserve is `ax.get_tightbbox` minus `ax.get_window_extent`, per side. `get_tightbbox` unions *everything the axes draws*, which matters for ov.pl specifically: `ov.pl.forest` writes its CI strings ~30 mm to the right of the axes. Measured directly:

| | forest annotation vs the next panel |
|---|---|
| cnsplots multipanel, unmodified | **overlaps the neighbour by 56 px** — it reserves for the decorations its own plots draw, not arbitrary text |
| panelflow | no overlap; the 30 mm is reserved; both boxes still exact |

That is the concrete reason this is native rather than a dependency: cnsplots is excellent for cnsplots' own plots, but fed ov.pl's decorations it collides, and depending on it would also pull in a heavy tree (lifelines, comprisk, gseapy, pycomplexheatmap, …) that omicverse deliberately keeps optional. panelflow adds **no dependency** — the suite passes with cnsplots absent.

## Agent-friendly by construction

`panel()` returns the axes and does **not** call `plt.sca`. A caller passes `ax=` explicitly; drawing into the wrong panel is a `KeyError` (`fl['Z']` lists the known labels), not a silent success. The engine only calls `set_position`, so it is agnostic to what drew into the axes — plain matplotlib, seaborn and ov.pl are each tested with the same geometry assertion.

`plt.gca()` is unchanged by `panel()` (saved/restored around construction and each call).

## How the size is guaranteed

`set_position` uses `panel.width / fig_w` directly, so the box never depends on a measurement — an unconverged layout has slightly wrong *positions*, never a wrong *size*. The draw handler re-lays-out and re-draws a bounded number of passes behind a re-entrancy flag (converges in one pass in practice). The panel tag is `set_in_layout(False)`, or it would be charged back into the reserve it is offset from and walk left on every pass.

## Documented limits (each pinned by a test)

- A fixed aspect (`pie`, `imshow`, `set_aspect('equal')`) genuinely contradicts a fixed rectangle; matplotlib shrinks the drawn box to the largest correctly-shaped one. `get_position(original=True)` still reports the assignment, and `adjustable='datalim'` or a square request gets the exact box back.
- `fig.colorbar(m, ax=panel_ax)` resizes its parent and the next layout pass undoes it — use a dedicated panel and `cax=`.
- Positions read before the first draw are provisional; wrapping depends on the measured reserves.

## Design credit

The flow-packing + measured-reserve approach follows [cnsplots](https://github.com/faridrashidi/cnsplots) (Farid Rashidi, BSD-3-Clause), credited in the module docstring. Implemented independently — no code copied, and the public API deliberately differs (explicit addressing, no implicit current-axes).

## Tests

`tests/pl/test_panelflow.py` — 33 tests, geometry measured (positions read back and converted to mm), not eyeballed. Red-test evidence: reintroducing the gridspec bug (subtract the reserve from the box) → 6 red; a static zero reserve → 4 red; measuring only the expected decorations rather than the tight bbox → forest lands on its neighbour. `tests/pl` + `tests/architecture` green with this on.

Companion, separate PRs: #930 sizes multipanel's panels within the gridspec model; #931 gives the remaining single-axes plots an `ax=` so they can go into a panel at all.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `519eee94a5a0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.