# Issue

**Title:** Use symlink to Xenium output morphology/transcripts files

## Description

When updating the Xenium Explorer, some large files (morphology/transcripts) are duplicated, creating unecessary large RAM usage.

This PR makes symlink to point to the original outputs of the Xenium machine.

> NB: this assumes that the Xenium output was read to `SpatialData` after this PR. If you already have an existing SpatialData object, simply add the absolute path to the raw Xenium data in the attrs, as follow: `sdata.attrs["xenium_output_path"] = "/path/to/xenium/output"`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e2a8473243a3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.