# Issue

**Title:** 3.0.7 Release

## Description

Updating torch dependencies due to security risk.

Torch 2.12.0
torch-geometric 2.8.0
torchvision 0.27.0
adjustments to ONNX model export method

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c13abe1c8441`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.