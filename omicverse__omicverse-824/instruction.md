# Issue

**Title:** ci: avoid uv run dependency resolution

## Description

ci: avoid uv dependency sync during lint and tests

Use `uv run --no-sync` for flake8 and pytest so CI continues to run
commands through uv without triggering an extra project dependency sync.
This avoids resolving optional extras such as `omicverse[full]`, which can
fail when unavailable packages like `dynamo-release` are not installable from
the current package index.

Also skip the automatic Claude review job for fork-based pull requests, where
repository secrets and OIDC permissions may be unavailable.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f096ef958f94`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.