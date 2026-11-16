# Issue

**Title:** refactor: consistent use_rep, use_raw, copy and keyword-only arguments, with deprecations

## Description

Summary: This PR makes the API of the 0.7.0 release consistent within the current argument naming (`key_added`, `inplace`, `use_rep`, `layer`). Every change keeps existing calls working, with a FutureWarning until 0.8.0.

Changes:
- `tl.ithcna` now takes `use_rep` as the suffix of the obsm key (`"cnv"`), like every other function. A full key such as `"X_cnv"` still works, with a FutureWarning.
- `tl.ithgex` now has `use_raw: bool = False`. In scanpy, `None` means "use raw if present", while here it meant "don't use raw". `None` still works as `False`, with a FutureWarning.
- `pp.neighbors`, `tl.leiden` and `io.read_scevan`:
  - With `inplace=False` they returned a modified copy of the AnnData, while every other function returns the result.
  - They now take `copy=True` for a modified copy.
  - `inplace=False` keeps returning the copy for now, with a FutureWarning that it will return the result from 0.8.0.
  - Passing both raises an error.
- Positional arguments:
  - A new decorator keeps positional calls working with a FutureWarning until 0.8.0. It applies to:
    - the options that the 0.7 refactor made keyword-only without a warning (`pp.neighbors`, `tl.leiden`, `tl.pca`, `tl.umap`, `tl.tsne`, `tl.copykat`), in their 0.6.1 order;
    - `groupby` in `tl.cnv_score`, `tl.ithcna` and `tl.ithgex`;
    - the result table argument of `io.read_scevan`.
  - `key` of `tl.spatial_regions` is new in 0.7, so it is keyword-only right away.
  - The rule: the objects a function reads or annotates stay positional (`adata`, and the input file or directory of io functions), and every option is keyword-only.
- Each change has a `versionchanged` or `deprecated` note.

Testing: New tests call `neighbors`, `leiden`, `pca`, `umap` and `tsne` with 0.6-style positional arguments and check the warning and the result. They also cover too many positional arguments, the `use_rep` and `use_raw` deprecations, and `copy` versus `inplace=False` in all three functions. The full suite passes on the cluster (475 passed, 12 skipped), and so do prek and mypy.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bc1693895a70`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.