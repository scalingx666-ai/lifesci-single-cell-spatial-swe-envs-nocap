# Issue

**Title:** Sc 51 aggregate

## Description

add aggregate_stats to RasterAggregator

```
from harpy.utils._aggregate import RasterAggregator

aggregator=RasterAggregator( mask_dask_array=mask, image_dask_array=image)
aggregator.aggregate_stats( stats_funcs=("sum", "mean", "count", "var", "kurtosis") )
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `392b7102930c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.