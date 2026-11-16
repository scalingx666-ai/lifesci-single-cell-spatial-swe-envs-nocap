# Issue

**Title:** Stain normalization: Reinhard color transfer

## Description

## Summary

First public surface for the experimental stain-normalization module (builds on #1178). Adds two method-dispatched entry points and implements the Reinhard (2001) color-transfer branch end-to-end:

- `fit_stain_reference(sdata, image_key, *, method="reinhard", scale="auto", method_params=None) -> StainReference`
- `apply_stain_normalization(sdata, image_key, reference, *, scale="auto", method_params=None, image_key_added=None) -> xr.DataArray | None`

Reinhard standardizes a source image by its own tissue statistics and rescales to a fitted reference, working in the Ruderman Lab space the foundations already provide. `macenko`/`vahadane` are recognized by the dispatch but raise `NotImplementedError`; the public signatures won't change when they land.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `38aa85e8fddd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.