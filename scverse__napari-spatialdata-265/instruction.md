# Issue

**Title:** fix contrast limits

## Description

Fixes the issue in #262 regarding calculating contast limits for MultiScale data. This PR checks whether data is multiscale and if so calculates the contrast limits based on the lowest resolution. Furthermore, an additional check is added to see whether contrast limits are monotonically increasing and if this is not the case it sets the contrast limits to the dtype range.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2d45606bf9d2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.