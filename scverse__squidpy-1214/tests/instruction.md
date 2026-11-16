# Issue

**Title:** ci: test Python 3.14

## Description

## What

Add **Python 3.14** to the `hatch-test` matrix in `hatch.toml` (stable + the pre-release variant), and move the pre-release job from 3.13 → 3.14 (newest), updating the macOS exclude to match.

```toml
# hatch.toml [envs.hatch-test]
matrix = [
  { deps = ["stable"], python = ["3.11", "3.12", "3.13", "3.14"] },
  { deps = ["pre"], python = ["3.14"] },
]
```

## Why

Squidpy already *declares* 3.14 support (`requires-python = ">=3.11"`, classifiers through 3.14), but the test matrix was pinned to 3.11–3.13, so **3.14 was never actually exercised**.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `83e6511a6f62`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.