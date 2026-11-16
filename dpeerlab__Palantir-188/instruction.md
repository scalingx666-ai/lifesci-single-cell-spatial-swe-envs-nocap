# Issue

**Title:** Pseudotime: several start cells, faster and leaner, finite far from waypoints (consolidates #185, #186, #187)

## Description

Consolidates the three open PRs by @Marius1311 together with the follow-ups from their review, which he agreed to on dpeerlab/Palantir#185 and dpeerlab/Palantir#186. Each PR's branch is merged unchanged with `git merge`, in this order, so his commits and authorship are kept:

1. **dpeerlab/Palantir#187: Fix NaN pseudotime when a cell is far from every waypoint** (`3ee85d2`). The waypoint weights are normalised with `scipy.special.softmax`, so a cell more than ~38 bandwidths from every waypoint no longer makes the pseudotime NaN for every cell.
   - Follow-up: the release note says the new weights equal the old ones up to floating-point rounding.
2. **dpeerlab/Palantir#186: Faster, leaner pseudotime on large data** (`f60cd10`). Parallel shortest paths, a chunked refinement, and `_connect_graph` via `scipy.sparse.csgraph`.
   - Merged with dpeerlab/Palantir#187, so each chunk of the refinement uses softmax.
   - Follow-ups:
     - shortest paths stay serial under the threading backend;
     - `D` is filled as blocks arrive (`return_as="generator"`, 4 blocks per job). The parent's peak while assembling `D` drops from 2.0x to ~1.4x of `D`. This makes joblib >= 1.3 a requirement;
     - networkx moves to the test extras.
3. **dpeerlab/Palantir#185: run_palantir accepts several early cells** (`6ae3cac`), addressing dpeerlab/Palantir#146.
   - Merged with dpeerlab/Palantir#186: every start row is held at 0 in the chunked loop.
   - Follow-ups:
     - a docstring for the several-start semantics;
     - a warning when snapping to the boundaries merges early cells;
     - a warning when automatic detection finds no terminal state;
     - `identify_terminal_states` accepts a list and takes `use_early_cell_as_start`;
     - the not-found error names only the missing cells;
     - tests for the warnings, the list input and the error message, plus a start-row hold test that fails if either hold is removed.

**Tested:**
- The full test suite passes (190 passed, 6 skipped).
- On several real datasets of up to 50k cells:
  - with one start cell, results agree with `master` within ~1e-15. The drift comes from the softmax in dpeerlab/Palantir#187 and from last-digit differences in dpeerlab/Palantir#186; dpeerlab/Palantir#185 and the follow-ups add no change at all, bit for bit;
  - dpeerlab/Palantir#186 gives the same bits with `n_jobs=1`, with 4 processes and with threads;
  - a cell far from every waypoint stays finite, where `master` returns NaN everywhere.

Thank you, @Marius1311, for dpeerlab/Palantir#185, dpeerlab/Palantir#186 and dpeerlab/Palantir#187, and for agreeing to the follow-ups. Your commits are kept as they are.

This supersedes dpeerlab/Palantir#185, dpeerlab/Palantir#186 and dpeerlab/Palantir#187.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f819d5156c8f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.