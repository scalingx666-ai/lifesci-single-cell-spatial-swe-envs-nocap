# Issue

**Title:** Fix scatterplot widget

## Description

Two notes:
- This PR is branched from the annotation widget branch but I couldn't open against it, this explains the long history (let's merge the annotation widget PR first).
- Tests and pre-commits pass locally.

In this PR I fixed/improved the scatterplot widget.
- [x] we can plot `.obs` again, there was a problem with `instance_key` not being set in the model;
- [x] I decreased the point size of the scatterplot since the plots were too cluttered; the point size can be adjusted from the configs;
- [x] I added a splitter widget to make it possible to resize the plot; before most of the widget space was occupied by the bottom widgets
- [x] I have tested all the components; all works except for one thing, described below.

The following is still broken:
- [x] when pressing export, the data was saved in `AnnData` object that was a copy, not the original table. To fix this we need to be able to access the table annotating the current layer. This should be fixed. @melonora could you please have a look at this? Please look at my comments in `_scatterwidgets.py` where I explain what I tried and what I observed.
- [x] For the moment I implemented a workaround: the "correct" table is searched by looking at the length of the annotation to save.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `60d4187e945c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.