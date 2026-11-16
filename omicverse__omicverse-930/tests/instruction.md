# Issue

**Title:** feat(pl): size the panels, not just the canvas, in multipanel

## Description

`width` plus `width_ratios` fixes the canvas and lets the panels fall where they may, so the panel that gets drawn depends on how much room the tick labels happened to need. A journal that specifies the **panel** — "each panel 45 mm wide" — cannot be satisfied that way.

This inverts the derivation: give the panels, and the canvas follows.

```python
fig, ax = ov.pl.multipanel((2, 3), panel_size=(45, 100))
fig, ax = ov.pl.multipanel((2, 3), panel_widths=[45, 60, 30],
                           panel_heights=[80, 50],
                           margins=(20, 6, 16, 10), spacing=(9, 7))
```

Measured, not assumed — the tests read the drawn axes back, because the arithmetic is only right if the conversion into gridspec's figure fractions is right:

| requested | drawn |
|---|---|
| `panel_size=(45, 100)`, 2x3 | every panel 45.00 x 100.00 mm |
| `panel_widths=[45,60,30]`, `panel_heights=[80,50]` | 45/60/30 x 80/50 mm, exact |

Exact to 0.05 mm, including asymmetric margins (a bigger left margin moves the panels, it does not shrink them) and unit round-trips (50.8 mm == 2.0 in).

**The tradeoff, stated in the docstring rather than discovered later:** this turns constrained layout off, because the two are contradictory — one reflows to fit content, the other refuses to. That makes `margins` load-bearing: anything outside the axes (tick labels, y-labels, panel tags) has to fit in them and is clipped rather than accommodated. Panel sizes also need a regular grid — a mosaic panel can span columns and so has no single width, and asking for one now says so instead of guessing.

## Two smaller additions

**`title` / `title_kw`** — a figure number is part of the figure. Writing `fig.suptitle` afterwards is easy to forget on exactly the panel that needed it.

**`panel_styles`** — per-panel settings, keyed like `axes`. `color_cycle` binds a cycle to the panel so the plotting calls that follow do not each have to carry the colour; every other key goes to `Axes.set`, so `title`, `xlabel`, `xlim` work.

```python
fig, ax = ov.pl.multipanel((1, 3), panel_widths=[45, 60, 30], panel_heights=[80],
                           title='Figure 1',
                           panel_styles={'a': {'color_cycle': ['#4C72B0', '#DD8452'],
                                               'title': 'Baseline'}})
```

A panel reachable under two keys (`'A'` and `'a'` on a mosaic) is styled **once**. Applying a prop cycle twice silently restarts it, which would put the first two lines on the same colour — visible only in the drawn figure, never in an error. There is a test for that specifically.

## Compatibility

Every addition is keyword-only and defaults to the previous behaviour. `tests/pl` is **577 passed, 2 skipped** — unchanged from master. Mosaics, plain grids, `label=False` position keys and the journal presets all behave as before, with explicit tests pinning each.

Contradictory inputs raise rather than silently picking one: figure size *and* panel size, `width_ratios` (relative) alongside `panel_widths` (absolute), a mosaic with `panel_size`, half a specification, the wrong number of column sizes, margins that leave no room, and `panel_styles` naming a panel that does not exist.

Every example in the `@register_function` entry was executed as written before shipping — a registry example that does not run is the failure mode this codebase has been cleaning up all week.

## Where this came from

Comparing our multipanel against [cnsplots](https://cnsplots.farid.one/latest/examples/showcase.html), which builds panels imperatively (`mp.panel("A", 45, 100)` sets an implicit current-axes, and the next plotting call draws into it). Our declarative-plus-named-addressing shape is better for a caller that cannot see the figure — drawing into the wrong panel is a silent success there and a `KeyError` here — but cnsplots was right about two things we lacked: panels sized in real units, and style bound to the panel rather than repeated at every call. Those are what this adds; the implicit current-axes is deliberately not adopted.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7d9b0423b778`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.