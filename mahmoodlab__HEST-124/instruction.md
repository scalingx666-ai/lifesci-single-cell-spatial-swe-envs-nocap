# Issue

**Title:** fix torch.amp.autocast

## Description

`torch.cuda.amp.autocast(dtype=precision)` will be deprecated soon -> `torch.amp.autocast('cuda')`

PyTorch Warning info page https://docs.pytorch.org/docs/stable/amp.html

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e52246def9a1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.