# Issue

**Title:** fix(pl): drop deprecated N argument to ListedColormap

## Description

## What

In `cluster_trends`, the per-covariate categorical colormap is built as:

```python
cm = ListedColormap(colors, N=len(colors))
```

Passing `N` to `ListedColormap` is **deprecated since matplotlib 3.11 and will be removed in 3.13** (`MatplotlibDeprecationWarning` at `src/cellrank/pl/_cluster_trends.py:173`).

## Fix

`N` equals the number of colors, so it's redundant — matplotlib defaults `N` to `len(colorlist)`. Drop it:

```python
cm = ListedColormap(list(colors))
```

`cm.N` (used on the next line for `imshow`) and the rendered output are unchanged.

## Validation

- Against **matplotlib 3.11.0rc2** (pre-release env): the `TestClusterTrends` covariate tests pass with the `ListedColormap` deprecation promoted to an error.
- On stable: `TestClusterTrends` → 14 passed (the 2 `cluster_lineage` image-comparison failures are the pre-existing transparent-background issue fixed separately in #1323).

> Independent of the other CI-fix PRs (#1322–#1325); a forward-looking fix so CellRank keeps working on matplotlib ≥3.13.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e32c1315dafe`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.