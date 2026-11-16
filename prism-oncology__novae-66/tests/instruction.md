# Issue

**Title:** Add a learning rate scheduler + minor docs updates

## Description

- Added a learning rate scheduler in `fit` and `fine-tune`. This should improve the model stability during training. It can be disabled using `use_scheduler=False`.
- Updated the default `fit`/`fine_tune` arguments: we now use `patience=4` and `min_delta=0.05` for slightly longer training by default.
- Misc docs updates (more advice, fix broken links, etc).
- Remove old deprecated functions.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c68baa5d3339`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.