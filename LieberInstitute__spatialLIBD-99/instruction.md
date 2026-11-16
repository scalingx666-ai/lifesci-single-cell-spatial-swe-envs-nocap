# Issue

**Title:** Improve layer stat cor plot

## Description

Adress #98 

- Used strict match instead of grepl to fix substring match bug in `create_annotation_matrix()`. 
- Add check for matching names in `rownames(cor_stats_layer)` and `annotation_df$cluster`
- Added test for `layer_stat_cor_plot()` - testing above (using 1,3, 13 example)
- Check for / used in reference labels in `annotate_registered_clusters()`
- Add test for `annotate_registered_clusters()`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `41866c225488`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.