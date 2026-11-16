# Issue

**Title:** Sc 45 instanseg

## Description

- adapt instanseg notebook, so it works with version of instanseg as in main branch
- move hp.im.instanseg_callable to public API
- write to intermediate zarr store in `hp.im.labels` to reduce ram memory and efficient processing
- write to intermediate zarr store if len( output_labels_layer) > 1 in `hp.im.segment`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `96f425baa5b5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.