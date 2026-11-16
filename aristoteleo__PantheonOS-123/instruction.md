# Issue

**Title:** store seed: upstream source-revision tracking + renamed-skill reconcile

## Description

## What

Seed-side half of the store provenance/freshness feature. Pairs with `pantheon-hub` PR #17 (new `source_rev`/review columns + transfer endpoint) and the `pantheon-ui` reviews/freshness PR.

### Source-revision tracking
- `_clone_repo` now returns the upstream commit it cloned (`git rev-parse HEAD` + commit date); factory content records this repo's HEAD.
- `source_rev` / `source_committed_at` flow through the manifest → `_publish_one` → publish/update payloads, so every package records which upstream revision it came from. The hub stamps `source_synced_at` on its side.

### check-updates
- `pantheon store seed check-updates` runs `git ls-remote <url> HEAD` per external source and compares to the `source_rev` the store holds: **up to date / BEHIND — upstream moved / no source_rev**. This is how the store "notices" upstream changes between re-seeds.

### Renamed/removed-skill reconcile
- After publishing, each source is reconciled: a package still in the store but absent from this run is an orphan (upstream renamed/removed it). If it carries reviews:
  - **content matches** a current package (`content_hash`) → it's a rename → reviews are auto-reclaimed via `transfer_reviews`;
  - **no match** → warn that reviews would be stranded, with the exact `reclaim-reviews` command to run.
- `pantheon store seed reclaim-reviews --from-name X --to-name Y` for manual recovery.

### Client
- `StoreClient.transfer_reviews()` + a `source` filter on `search()`.

## Testing
`_git_meta` verified on real checkouts; the full reconcile algorithm (paginate by source → content_hash match → transfer) exercised against a local dev hub (rename → reclaim moves the review and recomputes aggregates); `check-updates` validated against the 6 external sources' live HEADs.

## Note
Backward-compatible: all new payload fields are optional and ignored by an older hub. Existing packages show no `source_rev` until the next re-seed records it.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e5caa33ad8b8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.