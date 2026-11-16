# Issue

**Title:** chore(deps): bump rdkit to 2026.3.5 and codeql-action/upload-sarif to 4.37.6

## Description

Combines the two open dependabot PRs into one, rebased onto current `main` (65a2aa2):

- **#83** — bump `rdkit` from 2026.3.4 to 2026.3.5 (`uv.lock` only; the only version that changes is rdkit — remaining lock hunks are equivalent marker rewrites from dependabot's newer uv, and `uv lock --check` passes on the result)
- **#84** — bump `github/codeql-action/upload-sarif` from 4.37.4 to 4.37.6 in `.github/workflows/scorecard.yml` (pinned SHA + version comment)

Both original commits are cherry-picked with dependabot authorship preserved (`-x` annotated). The two changes touch disjoint files; no conflicts.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e06151ab36e8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.