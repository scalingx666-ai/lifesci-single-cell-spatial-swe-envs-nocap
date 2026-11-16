# Issue

**Title:** Multi-slide pooled fit_stain_reference

## Description

`fit_stain_reference` now accepts `image_key: str | list[str]` — a list pools several images' tissue pixels into one fit (one reference for a cohort in one SpatialData).

```python
ref = sq.experimental.im.fit_stain_reference(sdata, ["s1", "s2"], method="macenko")
```

`tissue_mask_key` takes an order-matched list (or `None` for the `{key}_tissue` convention). Single-image fit unchanged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `62b918841c8c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.