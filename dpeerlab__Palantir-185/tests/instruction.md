# Issue

**Title:** run_palantir: accept several early cells

## Description

Addresses #146. `run_palantir` takes one `early_cell`. The workaround suggested there, one run per root and then the minimum, takes the minimum over runs that were each rescaled to [0, 1] by their own maximum.

`early_cell` now also accepts a list:

- Each early cell is moved to its nearest diffusion-map boundary cell, as before (or used as is with `use_early_cell_as_start`). All start cells go first in the waypoints.
- `_compute_pseudotime` starts from the shortest-path distance to the nearest start cell, and the refinement holds every start cell at 0.

One start cell gives the same result as before. On the tutorial's marrow sample, pseudotime from the tutorial's early cell is bit-identical to `master`'s. With three start cells (the tutorial's and two random cells), the result agrees with the per-root minimum at Spearman 0.9955 over 4,142 cells.

Tests: a list of one cell gives the same result as the string; start cells at both ends of a line give a pseudotime that peaks in the middle; start cells in separate components of the kNN graph give a finite pseudotime; a missing early cell raises.

`identify_terminal_states` still takes one early cell; I can extend it here if you'd like.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f819d5156c8f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.