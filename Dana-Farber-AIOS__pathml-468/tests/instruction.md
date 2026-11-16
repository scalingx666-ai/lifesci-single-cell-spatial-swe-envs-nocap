# Issue

**Title:** Version 3.0.6

## Description

**Version 3.0.6**

- onnx to 1.21.0
- protobuf to 4.25.1
- Needed to make these updates due to security issues flagged with ONNX

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ce8ca7063d88`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.