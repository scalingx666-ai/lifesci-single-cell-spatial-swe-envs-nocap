# Issue

**Title:** ci: nightly store sync + auto-review workflow

## Description

## What

A GitHub Actions workflow (`.github/workflows/store-sync-review.yml`) that runs the store quality loop in the agent image:

```
seed check-updates  ->  seed prepare  ->  seed publish  ->  review --changed-only
```

i.e. pull upstream changes, re-publish changed skills (auto-versioned + rename-reconciled), then score only the new/changed skills as the **pantheon-reviewer** bot via the hub API.

## Safe rollout
- Ships **manual-only** (`workflow_dispatch`) with inputs: `source`, `skip_publish` (review-only), `review_limit` (cap cost on a first run).
- The nightly `schedule:` cron is **commented out** — enable it after a clean manual run against staging.

## Required repo secrets
| secret | purpose |
|---|---|
| `PANTHEON_HUB_URL` | target hub (staging first, then prod) |
| `STORE_PUBLISHER_USER` / `STORE_PUBLISHER_PASSWORD` | account that may publish store packages (seed) |
| `PANTHEON_REVIEWER_PASSWORD` | password of the `pantheon-reviewer` bot |
| `REVIEWER_ANTHROPIC_API_KEY` | LLM key the reviewer scores with |

## Depends on / prereqs
- The **automated reviewer** PR (adds `pantheon store review`) merged **and** the agent image rebuilt to include it.
- Hub deployed with review / `source_rev` / `evaluation` support; the `pantheon-reviewer` bot user created on the target hub.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `313c0dc91350`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.