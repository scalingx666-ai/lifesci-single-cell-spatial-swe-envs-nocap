# Issue

**Title:** refactor: add StainReference transform methods (2/4)

## Description

Experimental stain arc (2/4). Rebased onto `main` after #1279.

Makes the fitted reference a `StainFit` object and moves the apply operations onto it (`fit` -> `transform`/`decompose`):

```python
fit = sq.experimental.im.fit_stain_reference(sdata, image_key="he", method="macenko")
fit.transform(sdata, image_key="he")   # normalize      (was normalize_stains)
fit.decompose(sdata, image_key="he")   # per-stain maps  (was decompose_stains)
```

- `StainReference` -> `StainFit`; `normalize_stains` / `decompose_stains` free functions -> `StainFit.transform` / `.decompose`.
- `decompose` now requires a fitted `StainFit`. The old `decompose_stains(reference_or_method="macenko", ...)` fit-on-the-fly path (with `white_point` / `method_params` / `tissue_mask_key`) is dropped; fit explicitly first.
- Comparing or hashing a `StainFit` raises (array fields make value-equality ambiguous), matching numpy.

Experimental API, no deprecation.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d8a3195c7c4f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.