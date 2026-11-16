# Issue

**Title:** feat(pl): a general Sankey / alluvial plot

## Description

`ov.pl` had only `perturb_sankey` (perturbation-specific), so an ordinary two-level flow could not be drawn. `ov.pl.sankey` draws flows between two or more categorical columns into a given axes.

```python
ov.pl.sankey(tips, ['day', 'sex'], ax=ax)
ov.pl.sankey(tips, ['day', 'time', 'sex'])   # three-stage alluvial
```

Table-first like its neighbours — data-first, keyword-only `ax=` (draw into it when given, else its own figure; `figsize` ignored with `ax`), `palette=`, `order=`, returns the axes, no `plt.show()`. Ribbons are filled polygons on a closed-form smoothstep (flat at both ends), coloured by the left node so a source can be followed downstream. Patches carry gids so geometry reads straight off the artists.

**Mass is conserved by construction** — a ribbon's left width is `count(L,R)/N` scaled by the left stage's span, so summed over the right categories it collapses to the left node's height. Asserted from the drawn polygons to 1e-9; a guard test mutates a ribbon and confirms the check goes red (red evidence: scaling one width by 1.05 → 2 failed; reverted → 2 passed).

10 tests: in-place `ax=` with no new figure and no `gca()` leak (decoy-figure check), standalone figure creation, two- and three-column, mass conservation, unknown-column and <2-column errors.

Ribbon geometry follows [cnsplots](https://github.com/faridrashidi/cnsplots) (BSD-3-Clause), credited in the docstring; implemented independently.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7aa534379a68`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.