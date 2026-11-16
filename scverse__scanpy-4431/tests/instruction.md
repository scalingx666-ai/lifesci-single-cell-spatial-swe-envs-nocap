# Issue

**Title:** fix: set NaN density for tiny or degenerate groups in tl.embedding_density

## Description

> [!NOTE]
> **AI-assisted.** I wrote this change with an AI coding agent, and a separate AI review agent re-ran the tests described below. I review and test the final diff myself before marking it ready for review.


**LLM usage**

- [x] LLM or coding agent used: Claude Opus 5.5 via Claude Code
- [x] If one was used, I, a human, have reviewed, understood and tested every changed line
- [x] 
- [x] [Tests][] included or not required because:
- [ ] [Release notes][] not necessary because:

[tests]: https://scanpy.readthedocs.io/page/dev/testing.html#writing-tests
[release notes]: https://scanpy.readthedocs.io/page/dev/documentation.html#adding-to-the-docs

### What was wrong

`sc.tl.embedding_density(adata, groupby=...)` runs `scipy.stats.gaussian_kde` once per category.
A 2D KDE needs at least 3 points that do not all lie on one line or point.
Otherwise `gaussian_kde` raises: `ValueError` for a 1-cell category, `LinAlgError` ("singular data covariance matrix") for 2 cells, or for 3+ cells that are collinear or identical (which identical expression profiles can produce in e.g. diffmap/PCA coordinates).
One such category made the whole call fail.

### The change

- In the `groupby` loop, a category with fewer than 3 cells, or whose KDE raises `np.linalg.LinAlgError`, gets `NaN` for its cells.
- After the loop, one `UserWarning` lists those categories ("have too few cells or degenerate coordinates").
- The docstring says which categories get `NaN`.
- Added `PLR0915` to the existing `# noqa: PLR0912` on `embedding_density`; the extra lines push it over ruff's statement limit (same pattern as e.g. `marker_gene_overlap`).
- Release note fragment under `docs/release-notes/`.

The `groupby=None` path is unchanged.

### Tests

New `test_embedding_density_groupby_degenerate_group`, parametrized over a small category of 1 cell, 2 cells, 3 collinear cells and 3 identical cells, next to a 30-cell category.
It expects a warning naming the small category, `NaN` for its cells, and values in [0, 1] for the large one.

Commands run (Python 3.13, scipy 1.18.1, numpy 2.5.4):

- `python -m pytest tests/test_embedding_density.py -q` against the `main` source: the 4 new cases fail (`ValueError` for 1 cell, `LinAlgError` for 3 collinear and 3 identical, and for 2 cells a `RuntimeWarning: invalid value encountered in divide` that the test config turns into an error); the 4 existing tests pass.
- Same command on this branch: 8 passed.
- `prek run --files` on the three changed files: all hooks pass.
- `towncrier build --draft`: the fragment renders under "Bug fixes".
- A one-off script with a 30-cell group, a 1-cell group and a 3-cell collinear group: `sc.pl.embedding_density` runs for `group="all"`, `group="b"` and `group=["c"]`. In the legacy plot, the `NaN` cells are drawn light gray (`#d3d3d3`, the same colour as the out-of-group background) at the foreground dot size.

### Open questions

- Is `NaN` plus a warning the behaviour you want here, or would you rather raise a clearer error?
- Unused (0-cell) categories are also set to `NaN` and listed in the warning. Before this change they raised as well.
- In the plot, a `NaN` group has the same colour as the background and stands out only by its larger dot size. The v2 (holoviews) plot was not checked.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2d3cd565d91d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.