# Issue

**Title:** Fixes the colors on the lfc bidirectional color scale.

## Description

Some redundant code in `HeamtapCell.js` and `Markers/index.js` regarding construction of the D3 scale function. Tried wrapping it into a function but then React started complaining about changes to the number of hooks so I don't know what's going on.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `21ede142ba40`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.