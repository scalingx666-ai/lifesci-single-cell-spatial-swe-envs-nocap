# Issue

**Title:** Debug set_figure_params

## Description

Set `matplotlib` formats directly with `matplotlib` since`set_matplotlib_formats` is [deprecated](https://ipython.readthedocs.io/en/stable/api/generated/IPython.display.html#IPython.display.set_matplotlib_formats) in the earlier version of IPython.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `117ceb523c18`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.