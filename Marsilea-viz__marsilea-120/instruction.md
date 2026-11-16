# Issue

**Title:** doc: add missing docstrings to Upset and UpsetData

## Description

I added the missing docstrings on the public methods and properties of Upset and UpsetData. The issue called out add_intersections, add_sets_size, add_sets_label, the get_*_ax helpers, get_data, binary_table, sets_table, sets_size, and the sets_names, items, sets_attrs, and items_attrs properties. mark and reset were also undocumented, so I covered those too.

Each docstring follows the numpydoc Parameters / Returns style already used in the package, and the descriptions come from what the methods actually do. No runtime behavior changed.

Tests: 720 passed, 6 xfailed. ruff is clean, and the Sphinx docs build succeeded.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `05620dbe9441`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.