# Issue

**Title:** Update ComplexHeatmap version

## Description

* Update ComplexHeatmap version to 2.5.4; @pkharchenko  noticed there were problems with older versions and `ht_opt$message`, cf https://jokergoo.github.io/ComplexHeatmap-reference/book/a-list-of-heatmaps.html#change-parameters-globally
* Updated the documents as well for dev

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2e723d886890`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.