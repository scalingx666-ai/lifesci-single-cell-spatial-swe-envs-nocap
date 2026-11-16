# Issue

**Title:** Labels support for 0.4.19, points support for > 0.4.19

## Description

- labels require `colormap` instead of `color` from `0.5.0`
- points require `border_xxx` instead of `edge_xxx` from the latest `main` (unreleased, > `0.5.0`).

This PR assumes that the next released version of napari is `0.5.0` (the current is `0.4.19`). @melonora confirmed that this should be the case. If not, we need to adjust the version strings in this PR.

Also, with @melonora we discussed if napari should automatically accept both the old argument and the new argument, as we do with our deprecation decorator approach:  If it will, then we can remove the manual versions if-else checks added with this PR.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f47bd5293830`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.