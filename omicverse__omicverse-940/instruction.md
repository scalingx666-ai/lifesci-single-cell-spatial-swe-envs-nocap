# Issue

**Title:** feat(pl): detect overlapping tick labels at draw time and separate them

## Description

## The problem

Tick labels are the one piece of text on a plot whose crowding depends entirely on the physical size the axes ends up at. `Fri Sat Sun Thur` is comfortable on a 90 mm panel and a smear on a 40 mm one — and the plotting call cannot know which it will be, because a layout engine may resize the axes afterwards.

!
(x labels of a small boxplot panel running into each other; y labels of a short barplot doing the same)

## What this adds

`ov.pl.declutter_ticks(ax)` measures the drawn label boxes and, **only when they collide**, works through a ladder, stopping at the first remedy that clears it:

1. **rotate** — x-axis only, up to `max_rotation` (rotating y labels buys no vertical room)
2. **stagger** — alternate labels into a second row, one label height further out
3. **thin** — every 2nd, then 3rd, … up to `max_thin`

It deliberately does *not* do what `ov.pl.adjust_text` does: a tick label is anchored to its tick, so sliding it along the axis would make it point at the wrong value. The room has to come from the perpendicular direction — which is what staggering is.

## Wiring

Registered as a `draw_event` callback by default, because the verdict depends on final geometry. It re-runs on every draw and is idempotent.

`style_axes` calls it, so every `ov.pl` plot that adopts the house frame gets the pass for free (20 call sites across 9 modules). Opt out with `set_tick_declutter(False)` globally or `style_axes(declutter=False)` per axes.

## Two subtleties the tests pin

- **`get_xticklabels()` returns only the *visible* labels**, so a pass that hid some could not find them again — a panel thinned while small stayed thinned after being enlarged. Labels are collected from `get_major_ticks()` instead, and each pass resets rotation/stagger/visibility before re-deciding. `test_thinning_is_undone_when_the_axes_grows_again` covers this.
- **Staggering stores the label's original transform**, so repeated draws do not push labels further out each time. `test_repeated_passes_do_not_accumulate_offsets` covers this.

## Tests

`tests/pl/test_declutter.py` (9 tests) asserts the *outcome* — no two visible labels overlap — rather than which remedy was used, so the ladder can change without rewriting tests. Full `tests/pl/` suite: 692 passed.

Verified on the real case: an `ov.pl.boxplot` in a 1.5 inch panel overlaps with the pass off and does not with it on (it picks 90°).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8b1bd8a6113b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.