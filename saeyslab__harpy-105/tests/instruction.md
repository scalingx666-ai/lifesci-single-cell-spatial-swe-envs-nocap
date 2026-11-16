# Issue

**Title:** SC_55 instance check aggregate

## Description

instance check fixes bug when doing 

```
aggregator = RasterAggregator(image_dask_array=image, mask_dask_array=labels)
dfs = aggregator.aggregate_stats(stats_funcs=("mean" ))
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7c14ead41023`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.