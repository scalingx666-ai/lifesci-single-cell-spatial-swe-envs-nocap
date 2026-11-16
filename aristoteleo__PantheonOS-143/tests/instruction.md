# Issue

**Title:** fix(store): don't bundle large/binary data files into store packages

## Description

## Problem
4 OpenClaw-Medical skills fail to publish to **both** staging and prod because the seed bundles **every** file in the skill dir, including data artifacts:

| skill | bundled size | failure |
|---|---|---|
| trialgpt-matching | 105 MB (dataset JSON/JSONL) | 413 at ingress |
| spatial-transcriptomics-{agent,analysis} / stagent | ~19 MB (11 MB chroma.sqlite3 + plots) | publish timeout |

## Fix
`_bundle_skip_reason()` skips files over a **1 MiB** per-file cap or with a binary/data/archive/media suffix, applied **before** `read_text` at all 3 bundle sites (factory groups ×2, external repos). Skips are logged.

## Verified
- `py_compile` clean.
- Ran the filter against the live OpenClaw-Medical repo: the 4 skills drop to **128 KB–2.8 MB** (datasets/sqlite/plots dropped) → publish cleanly under the 50 MB ingress limit.
- Binary files were already excluded via UnicodeDecodeError, so existing bundles only change for skills that carried >1 MiB **text** data.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1b218c312b87`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.