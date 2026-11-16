# Issue

**Title:** fix: rctd info without the anndata 0.13 FutureWarning

## Description

`rctd info` read `anndata.__version__`, which anndata 0.13 deprecates, so every call printed a FutureWarning. It now uses `importlib.metadata.version("anndata")`. Checked in a clean py3.12 env (anndata 0.13.4): no warning, same output; CI green on 266a139 (the final tree is identical: the release-prep commit was reverted and goes in with the v0.4.0 tag).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9c8420c9af55`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.