# Issue

**Title:** Grid plotting

## Description

Grid plotting for normal scatter plots and shaded scatter plots. Layout keys can be either a single string or a list of strings. Same goes for color_by. Empty string in a color_by list is treated as plotting the graph with no argument (['leiden', 'gene1', ''])
The grid layout is defined by the n_columns argument. If you have 6 panels and select n_columns=3 you will get a 2x3 grid and n_columns=2 will give you a 3x2 etc..
With w_pad and h_pad you can modify the width and height padding between the plots in the grid. If none is provided it will automatically decide the padding to avoid overlap.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4d0f181b87f1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.