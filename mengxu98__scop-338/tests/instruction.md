# Issue

**Title:** Fix heatmap row label wrapping

## Description

## Summary

- add `row_names_wrap` to `GroupHeatmap()`, `FeatureHeatmap()`, and `NMFHeatmap()`
- wrap both ordinary row names and the feature callouts produced by `nlabel` / `features_label`
- preserve original feature and item identifiers while wrapping display labels only
- size the row-name area from the wrapped labels without changing `legend.position`

## Validation

- targeted test file: 13 expectations passed
- clean package installation completed
- rendered real `GroupHeatmap()`, `FeatureHeatmap()`, and `NMFHeatmap()` examples with long labels

Supersedes #337 after the implementation branch was renamed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5543f75c00a9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.