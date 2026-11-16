# Issue

**Title:** Fix spatial_key handling in var_by_distance

## Description

## Description

`tl.var_by_distance(spatial_key=...)` used the requested coordinate key for NaN detection but still read observation and categorical-anchor coordinates from `obsm["spatial"]`. Custom-only inputs therefore raised `KeyError`, coexisting keys produced distances from the wrong coordinates, and differing NaN positions could cause a row-count mismatch.

Use `spatial_key` for both coordinate reads. Add three regression scenarios using small synthetic AnnData objects: custom-only coordinates, coexisting keys with different coordinates (parameterized over categorical and explicit coordinate anchors), and NaN alignment with non-sorted observation names. The tests assert raw distances so normalization cannot hide an incorrect coordinate selection.

The branch also includes the unchanged 12-line documentation fix from #1324 (original commit `067456f427ba9bffb4a477dcc084ac36dfbe2df3`, with original authorship preserved). This corrects the class role for the NumPy `NDArray` data alias, resolving the three existing strict-build warnings observed in [this PR's initial ReadTheDocs build](https://app.readthedocs.org/projects/squidpy/builds/35352728/).

Related to #1055.

## How has this been tested?

- Confirmed all four new parameterized cases fail before the spatial-key fix.
- `python -m pytest tests/tools/test_var_by_distance.py -q`: **12 passed** on Python 3.13.
- Independent review and a separate run of the full test module: **12 passed**.
- `sphinx-build -M html docs docs/_build -W -E -a`: **passed with zero warnings** on Python 3.13 / Sphinx 9.2.0 after clearing stale generated documentation. Verified the rendered NumPy links on all three affected field pages.
- Independent review of the documentation patch verified the real NumPy inventory, unchanged visible text, and unchanged handling of unrelated references.
- Project pre-commit checks for all changed files and `git diff --check`: passed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dc82c7387341`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.