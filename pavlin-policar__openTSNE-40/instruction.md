# Issue

**Title:** Docs pt2 + transform fixes

## Description

##### Description of changes
This started out as just another improvement to the documentation, but I forgot to commit fixes to a new branch and I couldn't be bothered to rebase.

- Fixes `prepare_partial` sometimes crashing because we weren't getting the `k` neighbors properly
- Add `k` parameter to `prepare_partial` for initialization
- Remove early exaggeration phase from `transform` and change default parameter values.
- Transform wasn't behaving properly. It should be equivalent to embedding each new point individually, but in batch - so it's faster. This now works for BH. Can't be identical for FFT because the grid dimensions can differ when inserting one-by-one points.

##### Includes
- [X] Code changes
- [X] Tests
- [X] Documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a777f00956ec`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.