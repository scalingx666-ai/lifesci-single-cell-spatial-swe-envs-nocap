# Issue

**Title:** refactor(datasets): use the shared scverse-misc dataset registry + downloader

## Description

Replaces squidpy's internal pooch-based dataset registry/downloader with the shared infrastructure from [scverse-misc](https://github.com/scverse/scverse-misc) (`scverse-misc[datasets]>=0.1.1`).

- Public API unchanged: `sq.datasets.*` keep the same signatures and behavior.
- ~750 lines of duplicated registry/download code deleted; `pooch` is now transitive.
- `datasets.yaml` stays in squidpy; the `anndata` / `image` / `visium_10x` loaders register via `register_loader`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b8dff5dead89`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.