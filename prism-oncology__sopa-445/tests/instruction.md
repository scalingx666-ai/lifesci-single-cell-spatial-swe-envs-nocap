# Issue

**Title:** Add CLI command to cache the cellpose model

## Description

New `sopa cache cellpose` command to pre-download the Cellpose weights before segmentation (useful for parallel patch segmentation or offline HPC nodes).

It prints the model path (by default `~/.cellpose/models`) to stdout (so it can be used by the workflow manager in `nf-core/sopa` ), and `--model-dir` sets `CELLPOSE_LOCAL_MODELS_PATH`.

I factored the model initialisation out of `cellpose_patch` into `load_cellpose_model`, so the cache and the segmentation share the same logic.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f0b5a54e7174`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.