# Issue

**Title:** Release 2.9.1

## Description

## Release 2.9.1

A performance patch on top of 2.9.0, released so that piscem-infer 0.8.0 can depend on it. Results are bit-for-bit identical to 2.9.0.

- #1255: faster EM/VBEM component step (no per-incidence bounds checks or NaN tests). Plain EM is about 7% faster and VBEM about 4.5%; `quant.sf` is byte-identical.
- `docs/release-notes-2.9.1.md`.

`develop` is `master` plus these commits, so this merges cleanly.

**Please merge with "Create a merge commit"** (not squash), so `master` stays an ancestor of `develop`.

After merging, release with `scripts/bump_and_publish.sh 2.9.1 --publish` on `master`, then sync `master` back into `develop`.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_016brRcptooQkxWr6TyWnwAE

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4163bb524142`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.