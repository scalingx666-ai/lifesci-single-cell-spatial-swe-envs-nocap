# Issue

**Title:** Enable using a scale>0 in staining-based segmentation for CLI/pipeline

## Description

Enable using a scale > 0 in staining-based segmentation for CLI/pipeline

Adds a --scale option to sopa patchify image so staining-based segmentation (e.g. Cellpose) can run on a lower-resolution scale instead of always using the highest one. .

```bash
sopa patchify image tuto.zarr --scale "scale1"  ...
```

This is exposed through the Snakemake pipeline via a new scale key in the patchify config:


```python
patchify:
  scale: "scale"
```

Closes

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4fd905cb2609`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.