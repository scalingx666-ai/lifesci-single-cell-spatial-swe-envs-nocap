# Issue

**Title:** fix(space): enforce raw count inputs for cell2location and RCTD

## Description

## Summary

Route raw count layers into cell2location reference filtering, both likelihood registries and the RCTD input copies. Support explicit layer names; reject missing custom layers and non-finite, negative or continuous values without rounding. When the default counts layer is absent, X is accepted only if it is valid count data.

Restore the reference expression matrix after filtering, including failure paths, and detach AnnData views before temporarily replacing X to protect the caller’s parent data.

The change is limited to one implementation file and the existing cell2location/RCTD test modules. Starfysh coordinate changes, method-name normalization, unrelated messages and the standalone migration document have been removed.

## Compatibility

Normalized X may coexist with raw count layers. Existing raw-count X inputs remain supported. Both methods now fail explicitly when no valid raw counts are available, instead of silently fitting count likelihoods to normalized expression.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `41531a627523`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.