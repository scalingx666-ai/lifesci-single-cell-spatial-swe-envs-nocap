# Issue

**Title:** store: automated skill reviewer (`pantheon store review`) + rubric

## Description

## What

The **reviewer** half of the store quality loop — so a scheduled job can score new/changed skills after a `seed`. Pairs with the hub's review/`evaluation` support and a forthcoming GitHub Actions workflow.

### New
- **`reviewer.py`** — the versioned skill-review rubric (6 weighted dimensions + anchors, deterministic `overall`/`verdict`, output schema). Pure stdlib.
- **`batch_review.py`** — scores skills via the Anthropic Messages API (tool-forced schema → always rubric-valid), writes results back:
  - `--write api` (default): POST as the **pantheon-reviewer bot** — works against dev SQLite *or* prod Postgres.
  - `--write db`: direct SQLite (dev only).
  - `--changed-only`: only re-review skills whose `content_hash` changed since their last review (stamped as `reviewed_content_hash`) → **nightly runs are near-free**.
  - `--only a,b`: restrict to specific names (e.g. exactly what `seed publish` just changed).
- **`pantheon store review`** CLI command.
- factory skill **`meta/skill_review.md`** — the rubric as a discoverable store skill.

### Fixed
- `seed check-updates` is now reachable from the CLI (the `StoreSeed.check_updates` method shipped in #123 but the `seed()` dispatch only handled prepare/publish).

### Client
- `StoreClient.submit_review()` + `get_reviews()`.

## The loop (each runs an existing CLI command)
```
pantheon store seed check-updates                 # which sources moved
pantheon store seed prepare && ... seed publish   # changed sources: pull, auto-version, reconcile
pantheon store review --changed-only --source all # review only new/changed skills
```

## Testing
Verified end-to-end against a local dev hub: review writes via the bot API with `reviewed_content_hash`; bumping a skill's content makes `--changed-only` re-review **only** that skill and skip the unchanged one.

## Note
No new deps (stdlib + the existing client). The reviewer needs `ANTHROPIC_API_KEY`; `--write api` needs the `pantheon-reviewer` bot creds.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `313c0dc91350`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.