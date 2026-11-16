# Issue

**Title:** fix radii of transformed circles

## Description

The calculation for the radii of transformed circles was wrong. This was manifested for instance when switching between the `global` and `downscaled_hires` coordinate systems in Visium.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `803c35e632eb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.