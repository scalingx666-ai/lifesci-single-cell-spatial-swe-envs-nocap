# Issue

**Title:** feat(pl): give the single-axes plots an ax= so any of them fits a panel

## Description

`ov.pl`'s table-first plots mostly accept `ax=` and draw into it. A handful did not — they silently created their own figure — so you could place `barplot` into a panel of `multipanel` but not `boxplot`, with nothing in the namespace marking which was which until the second one popped a stray window.

Four functions now take a keyword-only `ax=None`: `boxplot`, `plot_boxplot`, `plot_network`, `plot_grouped_fractions`. They follow the convention the siblings already use (`_new_axes`) — draw into `ax` when given, else `plt.subplots(figsize)`; `figsize` is ignored once `ax` is passed; no `plt.show()`.

**Return shape is unchanged by `ax`.** `boxplot` returns `(fig, ax)` with or without it — returning a bare axes when `ax` is passed would break `fig, ax = ov.pl.boxplot(...)` for anyone who adds the argument.

**Two leaks fixed, both of which only bite inside a panel:**
- `boxplot` drew its jitter with `plt.scatter` — onto `gca()`, i.e. the wrong figure when the panel is not current.
- `plot_network` called `plt.legend` / `plt.gca()`.

Both now target the supplied axes. The regression test opens a **decoy figure after the panel** and asserts nothing landed on it; without the decoy the test is worthless, because the panel is normally `gca()` and the leak is invisible.

`boxplot` also gained `x=`/`y=` as aliases for `x_value`/`y_value` (the siblings use `x`/`y`). Old names still work; passing both spellings with different values raises.

A guard test re-runs a "declares `figsize` but not `ax`" sweep over `ov.pl.__all__` and fails on any new single-axes plot that forgets `ax`, with an allowlist of the genuinely-composite functions — so a newly added plot cannot regress this silently.

`tests/pl` = 598 passed (577 + 21 new), 2 skipped — baseline unchanged. Red-test evidence: removing the `ax` guard in `boxplot` → 6 red; forwarding `figsize` to pandas alongside `ax` → 1 red; dropping `ax=ax` from the networkx draw calls → 1 red. All restored green.

Not changed, reported for follow-up: `complexheatmap` / `upset` / the marsilea-backed heatmaps are genuinely multi-axes (main panel + dendrogram + colour bar) and need a `SubplotSpec` / `SubFigure` hook, not a single `ax`; `plot_cellproportion` forwards to `cellproportion`, whose own `ax=` path still leaks labels through `plt.xticks`. Those are separate.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7d9b0423b778`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.