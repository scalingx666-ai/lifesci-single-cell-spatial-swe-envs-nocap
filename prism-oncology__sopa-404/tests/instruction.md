# Issue

**Title:** Nimbus

## Description

Nimbus aggregation is now available through `sopa.aggregation.nimbus`.

This function runs Nimbus on segmented cells and returns an AnnData object containing predicted marker intensities (cells × markers).

```
anndata = sopa.aggregation.nimbus(sdata, image_key="raw_image")
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `513227f38a4d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.