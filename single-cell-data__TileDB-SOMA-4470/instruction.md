# Issue

**Title:** [r] Fix for blockwise reading

## Description

Fix bugs in blockwise iteration in tiledbsoma-r

 - `read_next()` previously would reset the dim point after each `reset()`
 - minor-axis re-indexer was always built over the full domain instead of the requested coordinates

New SOMA methods:

 - `CoordsStrider$is_full_domain(extent = )`: check to see if this coordinate strider occupies the full domain (`extent`)
 - `CoordsStrider$full_coords`: active binding to realize the full span of the coordinate strider without advancing

Closes [SOMA-990](https://linear.app/tiledb/issue/SOMA-990/somasparsendarraydollarreaddollarblockwise-drops-coordinate)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `beb72a267248`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.