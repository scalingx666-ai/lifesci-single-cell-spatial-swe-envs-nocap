# Issue

**Title:** fix(pl): venn on matplotlib-venn, and volcano axis labels follow rcParams

## Description

Two chrome defects that make `ov.pl` plots look wrong in a multi-panel figure — both surfaced building a Nature-style 18-panel showcase.

**`ov.pl.venn`** drew through venny4py: non-proportional ellipses whose set names overlap the region counts. Now dispatches on set count — 2 or 3 sets go through **matplotlib-venn** (proportional circles, clean labels, the way cnsplots does it), >3 falls back to the old backend, <2 raises. Subset-count and set-label fonts follow `rcParams['font.size']` (or explicit `fontsize=`) instead of a fixed 3.5. matplotlib-venn guarded with an actionable ImportError. Also: the decorator's example passed `figsize=`, a parameter the function never accepted (would error) — added it.

**`ov.pl.volcano`** set its axis labels from `titlefont` (default size 14), so `log2FC` / `-log10(qvalue)` rendered at a fixed 14pt regardless of the panel — wildly larger than a 5-6pt figure. Added `label_fontsize` (default `rcParams['axes.labelsize']`) and routed `ticks_fontsize` to `rcParams['xtick.labelsize']`. Mathtext styling unchanged; only the size is decoupled. No data/threshold/colour/gene-label/return changes.

Before/after: venn labels no longer overlap and circles are proportional; volcano axis labels measured at 6pt under `axes.labelsize=6` (was 14).

Design credit: the matplotlib-venn approach follows [cnsplots](https://github.com/faridrashidi/cnsplots) (BSD-3-Clause). 8 new tests, `tests/pl` green (566). Red-checked: reverting either fix fails its tests.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a499589ea045`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.