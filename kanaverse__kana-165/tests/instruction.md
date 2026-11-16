# Issue

**Title:** Switch to gesel as the source for feature sets.

## Description

Need to adjust UI to:

- [x] collection names are now reported with the set details, given that the sets from all collections are now concatenated together. The parent collection for each set is contained within the `sets.collections` property from the FSE callback.
- [x] Shift collections from selectize to a gesel-like checkbox select.
- [x] Only gene sets with at least one overlapping genes will be returned by `computeEnrichment`; need to use the `set_ids` indices to get the details of each set, from the `sets.names` + `sets.descriptions` property from the FSE callback.
- [x] Consider showing a `(count/overlap)` text for each feature set.
- [x] MSigDB gene sets will now show up, so good opportunity to replace their descriptions with links. Guess you could also add links for the GO titles to Amigo like I do in [`gesel-app`](https://github.com/LTLA/gesel-app/blob/d2b6eeeb2b7dc230e29cafb16568909e1ee5687f/src/App.js#L455).

On the plus side, the sets are now sorted by p-value, so you don't have to do that.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0ddf5f61d914`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.