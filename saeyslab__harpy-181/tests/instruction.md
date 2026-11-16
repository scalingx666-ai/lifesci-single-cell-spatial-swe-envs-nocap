# Issue

**Title:** Sc 85 extract cupy

## Description

- update return type of harpy.tb.extract_instances
- add cupy support for harpy.tb.extract_instances
- add PyTorch dataloader that allows streaming from zarr store
- add notebook

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cf31bab5eba4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.