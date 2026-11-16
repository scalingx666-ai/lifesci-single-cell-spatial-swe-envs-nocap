# Issue

**Title:** fix(pl): volcano threshold guides are annotations, and ns gets a legend key

## Description

Two defects, both visible the moment a volcano sits beside other panels.

## The guides outweighed the data

The fold-change and p-value guides were fixed at **2 pt solid black**. At that weight three black bars dominate the points they exist to annotate — in a small panel they read as the panel's content rather than as an annotation.

Now a thin grey dash by default, drawn at `zorder=0` behind the points, with `threshold_color` / `threshold_linewidth` / `threshold_linestyle` to style them and `show_thresholds=False` to omit them.

## The grey majority had no legend key

The legend listed only `up:` and `down:`. Non-significant genes are usually most of what is plotted, so the grey cloud filling the middle of the figure was unexplained. `ns:<count>` is now included; `show_normal_in_legend=False` restores the old two-entry legend.

## Tests

`tests/pl/test_venn.py` — guide weight and colour, styling them, switching them off, and the legend keys. Reinstating the old defaults (2 pt black, no ns) fails the first and last of those, so they pin real behaviour rather than passing vacuously.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3a77b4ffa11b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.