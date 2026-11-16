# Issue

**Title:** fix(store): skill_search_store falls back to lexical when /recommend is unavailable

## Description

## Problem
`skill_search_store` calls `/api/store/recommend` (semantic). If that endpoint is unavailable — e.g. a store backend without pgvector/semantic search returns **404** — it hard-failed and handed the agent a raw error (`store search failed: Client error '404 Not Found' …`) with **zero results**, dead-ending discovery. Observed against the local dev hub (SQLite, no `/recommend`).

## Fix
On **any** `/recommend` failure, fall back to a **lexical keyword search** via `/api/store/packages?q=…&type=skill` and return those candidates — flagged `degraded: "lexical"` with a hint that the reviewer verdict/best_for signals aren't available, so the agent judges fit from the description. Only if the lexical call *also* fails does it return an error (with both causes).

Net effect: store discovery works against **any** store backend (semantic or not) instead of erroring out. No change to the happy path (semantic `/recommend` still preferred and returns the full reviewer payload).

Verified: local `/api/store/packages?q=segmentation` returns 34 skills, so the fallback yields real candidates where `/recommend` 404s.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6df814bb8843`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.