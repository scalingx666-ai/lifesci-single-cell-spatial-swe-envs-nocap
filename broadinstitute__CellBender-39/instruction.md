# Issue

**Title:** Update docker image with new CUDA version

## Description

... for updated pytorch compatibility.

The newer image also includes a few CellBender improvements, including reading and writing gene IDs in addition to gene names.  This is better practice in general, and also allows for improved compatibility with `scanpy`, which expects gene IDs in its `read_10x_h5()` method.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5db491041e02`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.