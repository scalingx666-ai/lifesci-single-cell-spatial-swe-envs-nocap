# Issue

**Title:** store CI: sync staging+prod nightly + local content-hash pre-filter

## Description

## What

**1. Run store-sync-review against both staging AND prod, nightly**
- Matrix over `{staging, prod}`; the two service accounts (store-seed / pantheon-reviewer) now share one password across both envs, so one set of secrets authenticates against either.
- `fail-fast: false` + per-env concurrency so one hub never blocks the other.
- Enables the nightly schedule (07:00 UTC). Verified: both legs green against staging + prod.

**2. Local content-hash pre-filter (perf)**
`seed publish` used to walk all ~2100 packages every run and, per package, blindly POST the full content twice (create + version) just to let the Hub reject identical content — ~3-4 round-trips + a 0.2s throttle each = 30-50 min for a no-change sync.

Now it diffs locally:
- One bulk `GET /packages` (`_fetch_hub_index`) pulls metadata + `content_hash` (the list omits the heavy content/readme).
- `_content_fingerprint()` replicates the Hub's `content_hash` byte-for-byte — **verified 40/40 against the live store** (files path included).
- Unchanged + metadata in sync → SKIP with zero requests; metadata drifted → one PUT; content changed → new version; new → create. Falls back to the old try-create-then-lookup if the index can't be fetched, so correctness never depends on the optimization.

Expected: nightly drops from ~30-50 min to ~1-2 min; Hub write load / 502s drop with it.

## Verified
- Hash replication 40/40 vs live store; index pagination complete across skill/team/agent.
- `py_compile` clean; both CI legs succeeded on staging + prod.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d2e7b1187425`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.