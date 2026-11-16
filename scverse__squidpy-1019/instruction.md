# Issue

**Title:** Add SpatialLeiden as clustering method

## Description

Close #879 

Added support for `spatialleiden` as a flavor in `sq.gr.calculate_niche`, following up on the idea mentioned in #879. The method is now integrated via the `flavor="spatialleiden"` option, wrapping the `spatialleiden.spatialleiden()` function.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d4f256f03d7e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.