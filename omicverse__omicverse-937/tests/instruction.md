# Issue

**Title:** feat(pl): adjust_text — label repel that cannot leave the axes

## Description

## The problem

The packaged `adjustText` places labels against the axes geometry it sees at call time. In a small axes it pushes labels clean out of the data limits. Measured on a 64×78 mm volcano panel sized by a layout engine, eight gene labels landed at data-y ≈ −6 against a y-limit of −0.5 — rendered below the x-axis and off the canvas.

Nothing about the call is wrong; the axes is simply too small for the repulsion it computes, and there is no invariant stopping it. That makes gene labels unusable on any volcano that is a panel of a larger figure.

## What this adds

`ov.pl.adjust_text` does the same job — separate overlapping labels, keep them near their points, draw leader lines — with one invariant added:

**every label is clamped inside the axes rectangle on each iteration.**

That makes it safe to call *after* a layout engine has resized the axes, which is exactly when the packaged version fails. No new dependency.

```python
texts = [ax.text(x, y, name) for x, y, name in top_genes]
ov.pl.adjust_text(texts, ax=ax)
```

The relaxation runs in display space: labels push apart along whichever axis they overlap less on, a gentle pull toward the anchor stops them drifting, and thin leaders connect each label to its point.

## Tests

`tests/pl/test_adjust_text.py` — the clamp (labels crowded at the top edge of a 2×2 inch axes stay inside), overlaps reduced, leaders drawn, empty input a no-op.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c29fe1d0b3b0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.