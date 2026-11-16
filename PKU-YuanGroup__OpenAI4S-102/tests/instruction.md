# Issue

**Title:** fix(review): scope a finding's identity to its review, not to its content

## Description

## Summary

A finding's **identity** was its content, and its content is also its **fingerprint**. Those answer different questions, so making them the same key broke both.

`review_findings.finding_id` is a global `PRIMARY KEY`, and it was derived from content alone:

```python
fingerprint = sha256(f"{severity}|{category}|{claim_ref}|{','.join(evidence_refs)}")
finding_id  = f"fnd-{fingerprint[:16]}"
```

So two sessions that reached the same conclusion collided. The second one's `complete_review` insert raised `UNIQUE constraint failed: review_findings.finding_id`, the transaction rolled back, its Auto Run stayed in `reviewing` — not a terminal status — and `start_run` then refused every later turn on that branch. The finding most likely to recur across sessions is a recurring wrong claim, so the collision landed on exactly the case worth catching. Reproduced on a real daemon, not just in a test.

### The fix, and why not the obvious one

`finding_id` is now `sha256(review_run_id | fingerprint)` and stays a global `PRIMARY KEY`. The content-only fingerprint is untouched — the auto-repair loop compares fingerprints across rounds to notice a finding did not go away.

Scoping the **id** rather than the **primary key** is what keeps every reader correct. Global uniqueness is load-bearing in two places a composite `PRIMARY KEY (review_run_id, finding_id)` would have broken:

- session import resolves a finding's owner with `SELECT run_id FROM review_findings WHERE finding_id=?`
- `repair_runs.finding_ids_json` stores bare ids

The table already declares `UNIQUE(review_run_id, fingerprint)`, so the new derivation is injective over the rows that can exist.

**No schema change, therefore no migration.** Every runtime reader already scopes by `run_id` (usually plus `candidate_id`); `_assert_verified_locked` never reads `finding_id` at all. Databases already stranded self-heal: the wedged run carries the dead daemon's `owner_instance_id`, so boot-time reconciliation abandons it.

### Two more things the audit turned up

**A storage failure escaped as a bare exception.** `shadow_after_turn` caught only `(AutoModeConflictError, ValueError, PermissionError, KeyError)`, so `sqlite3.IntegrityError` escaped, the gate discarded the whole result far upstream, and the turn reported `review_unavailable (review_did_not_run)` for a review that had reached a verdict. Broadened, with `record_diagnostic` on each. Swallowing is safe because it is not silent about the outcome: with no durable review, `_assert_verified_locked` refuses the promotion.

**A third writer disagreed.** The review *step* embeds the findings in its output JSON and is persisted *before* the findings table, so assigning ids at storage time left the step quoting an id that existed in no table. Binding now happens once, before any writer, and is idempotent.

The two original fixes are **not redundant** — I checked by mutating each back independently. Reverting only the identity still strands the second run in `reviewing`, because `terminate_auto_mode_run` will not close a run whose review never completed. Reverting only the exception handling lets `IntegrityError` escape bare again.

> [!NOTE]
> Stacked on #101 only because the exception-handling change touches `close_review_run`, which #101 introduces. **The substance is independent of that PR's contested ordering** — the bug is present on the target branch today and is worth fixing regardless of how #101 is resolved. Happy to port these two commits onto the target branch's `_persist_auto_mode` shape and open them standalone; it is a small change.

## Area

- [x] Server / gateway / API
- [x] Store / provenance / artifacts
- [x] Tests / harness / CI
- [x] Docs

## Change Type

- [x] Bug fix

## Verification

Ran:

```text
uv run pytest                                          5904 passed, 11 skipped, 0 failed
uv run python scripts/capture_response_schemas.py --check    exit 0, no breaking change
uv run python scripts/capture_response_contract.py --check   191/191 routes
uv run python -m harness.cli run --tier pr --offline         38/38
uv run python scripts/check_directory_readmes.py             green
uv run pre-commit run --all-files                            green
real-daemon reproduction: two frames, one daemon, identical reviewer finding
  6 findings | 5 distinct fingerprints | 6 distinct ids
  both runs completed_with_issues | IntegrityError count: 0
mutation checks: each of the three fixes reverted independently, each caught
  by its own test
```

Not run:

```text
a migration, and any backfill of existing rows
```

Reason:

```text
The schema is unchanged, so there is nothing to migrate. Existing rows keep
their old content-derived ids and cannot collide with the new scoped ones.
Databases already wedged by this bug are cleared by the boot-time
reconciliation already on the target branch, covered by
test_reconcile_moves_a_crashed_run_to_review_unavailable.
```

## Risk and Reviewer Focus

The identity change is the whole risk: if `finding_id` stopped being globally unique, session import's owner check and `repair_runs.finding_ids_json` would both silently resolve the wrong row. The argument that it stays unique rests on the pre-existing `UNIQUE(review_run_id, fingerprint)` constraint — please check that reasoning first.

Second, the broadened `except Exception` clauses. They are deliberate, but they are the kind of change that hides a future bug if the fail-closed path downstream ever stops being fail-closed.

## Checklist

### Diff Readiness

- [x] I reviewed and understand the full diff.
- [x] This PR is small and single-purpose.
- [x] No unrelated formatting, broad rewrite, or drive-by refactor is included.
- [x] Hotspot files were edited surgically if touched.
- [x] `openai4s/server/webui/vendor/` and `tests/fixtures/` were not reformatted.

### Tests

- [x] Relevant tests or manual checks were run and listed above.
- [x] No new test requires live LLM, network, GPU, SSH, Docker, lab hardware, or secrets in the default offline suite.
- [x] No tests were deleted without tracked replacements.
- [x] Kernel / host-RPC / gateway changes include focused contract coverage or a documented smoke test.

### Core Dependency Policy

- [x] No hard third-party import was added to the core engine, LLM client, or stdlib web server.
- [x] Optional science imports are guarded by `try/except ImportError` at every in-tree use site.
- [x] New dependencies, if any, are documented and justified.

### Public Disclosure and Security

- [x] No secrets, API keys, tokens, real credentials, private data, model weights, or local absolute paths are included.
- [x] No unpublished research roadmap, internal assignment, benchmark detail, or unreleased experimental result is disclosed.
- [x] Security-sensitive changes include appropriate synthetic tests or manual verification notes.
- [x] Docs do not overstate isolation, sandboxing, privacy, or security guarantees.

### Docs

- [x] Docs match actual code behavior.
- [x] User-facing behavior changes are reflected in docs or release notes where appropriate.
- [x] `README.md` and `README_zh.md` stay in sync where translated sections are affected.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6bd1b8b267b0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.