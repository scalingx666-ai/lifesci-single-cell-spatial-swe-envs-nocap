# Issue

**Title:** allow chunks none, threshold align labels

## Description

- Bug fix when chunks=None in hp.im.segment, and labels_layer_align is not None.
- support for threshold in hp.im.align_labels_layer

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `75b6d502aba7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.