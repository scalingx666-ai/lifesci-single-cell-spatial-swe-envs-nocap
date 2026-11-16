# Issue

**Title:** Modernize cache step in GitHub Actions

## Description

Modernize cache step in GitHub Actions as currently the use of v1 is
failing all builds [1].

Also put variables directly in `format!` directives, which apparently is
a thing now, and which Clippy will complain about if not done.

[1] https://github.com/brandur/redis-cell/actions/runs/15657611871/job/44110741744

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c7c0189f13a0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.