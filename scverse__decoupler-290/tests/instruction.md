# Issue

**Title:** Allow volcano() top to accept gene names

## Description

## Summary
- The `top` parameter in `pl.volcano()` now accepts a `str` or `list[str]` to annotate specific genes on volcano plots, in addition to the existing `int` behavior (top N by p-value)
- Missing gene names are reported in the assertion error message
- Bump version to 2.1.5

Supersedes #288 (rebased on updated main).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `df101b495dea`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.