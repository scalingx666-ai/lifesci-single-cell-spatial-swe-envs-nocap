# Issue

**Title:** perf(space): cut co_occurrence peak memory 622 MB -> 3.4 MB (4000 spots)

## Description

## TL;DR

- This PR lowers the peak memory of `ov.space.co_occurrence` in `omicverse/space/_neighborhood.py`.
- It builds the distances in small row blocks and keeps only the cluster-pair counts per radius.
- `tracemalloc` peak for 4000 spots, 8 cell types, `interval=6`: 622.3 MB -> 3.4 MB (99.4% less).
- `pytest tests/space/test_neighborhood.py -k co_occurrence -q` gives 1 passed, 1 skipped, the same as on `master`.

## What & Why

Before, `co_occurrence` built the full n x n distance matrix with `scipy.spatial.distance_matrix`. For each radius it then made an n x n boolean mask, called `np.nonzero` on it and counted pairs with `np.add.at`. At 4000 spots this held about 600 MB at once, and the memory grows with the square of the spot count.

Now the function drops unlabelled spots first, because they never form a pair. It then computes the distances for a block of about 65k pairs at a time. For each block it keeps the non-zero distances and their cluster-pair index, and counts the pairs inside each radius with `np.bincount`. Only a small `(n_steps, n_clusters**2)` integer table stays in memory.

The output stays identical. The distance formula is the same `distance_matrix` call, so pairs on a radius boundary are counted the same way. Zero-distance pairs and unlabelled spots are still excluded. The integer counts convert to the same float64 values that `np.add.at` gave, and the probability code after the counting does not change.

## Results

Peak traced memory (`tracemalloc`) and median wall time of one `co_occurrence(..., copy=True)` call on random spots in a 6000 x 6000 square, one CPU core:

| Situation | Before | After | Change |
|---|---|---|---|
| 200 spots, 4 types, interval=6 (small) | 1.52 MB, 3.4 ms | 1.31 MB, 2.0 ms | 14% less memory |
| 1000 spots, 8 types, interval=6 | 38.3 MB, 101 ms | 3.3 MB, 47 ms | 91% less memory, 2.2x faster |
| 4000 spots, 8 types, interval=6 | 623.2 MB, 1465 ms | 3.5 MB, 670 ms | 99.4% less memory, 2.2x faster |
| 4000 spots, 8 types, interval=50 | 623.2 MB, 9106 ms | 3.5 MB, 2827 ms | 99.4% less memory, 3.2x faster |
| 8000 spots, 8 types, interval=6 | 2518 MB, 5770 ms | 3.8 MB, 2690 ms | 99.8% less memory, 2.1x faster |

Small inputs gain little, because the old matrix was already small. No case uses more memory or runs slower. The peak memory now stays almost flat as the spot count grows.

## Why this is safe and easy to maintain

The change is one short loop in `co_occurrence` that replaces the full matrix and the per-radius masks. It still uses `distance_matrix`, so the distance values are the same. The returned occurrence array and interval edges are unchanged. `tests/space/test_neighborhood.py` covers the output shape and the parity with squidpy.

## Validation

- Benchmark: one call on 4000 spots, 8 cell types, `interval=6`, with a few duplicate spots and a few unlabelled spots. Peak traced memory was 622,334,085 bytes before and 3,442,265 bytes after, in three separate runs. Each run also checked that the occurrence values, edges, dtypes and shapes match the unmodified code.
- Tests: `pytest tests/space/test_neighborhood.py -k co_occurrence -q` gives 1 passed, 1 skipped (squidpy parity; squidpy is not installed), 23 deselected, the same as `master`.
- Reproduce:

```python
import tracemalloc, numpy as np, pandas as pd, anndata as ad, omicverse as ov
rng = np.random.default_rng(0)
adata = ad.AnnData(np.zeros((4000, 2), dtype=np.float32))
adata.obsm["spatial"] = rng.uniform(0, 6000, (4000, 2))
adata.obs["ct"] = pd.Categorical(rng.choice([f"c{i}" for i in range(8)], 4000))
ov.space.co_occurrence(adata, "ct", interval=6, copy=True)  # warm up lazy imports
tracemalloc.start(); ov.space.co_occurrence(adata, "ct", interval=6, copy=True)
print(tracemalloc.get_traced_memory()[1] / 1e6, "MB")
```

## AI assistance

This PR was prepared with AI assistance from Aiden. Candidates were tracked with Weco Observe.

Weco share link: https://dashboard.weco.ai/share/6OD6678RBttWfhEBZ1gRqTRB7z4iKRT2

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d94cf1da2d71`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.