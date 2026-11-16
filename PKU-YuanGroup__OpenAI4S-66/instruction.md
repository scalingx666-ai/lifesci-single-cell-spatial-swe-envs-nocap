# Issue

**Title:** fix(contract): stop publishing a thread race as the example-session shape

## Description

## Summary

`docs/response-schemas.json` froze `POST /example/session [ok].error` as
`string`. The field is `str | None`: `gateway.py` builds **one** dict literal for
both verbs and the value is `runner.example_seed.last_error()`. The sibling entry
`GET /example/session [ok]` already said `["null","string"]` — the same payload,
disagreeing with itself one key away.

The cause is a race, not a stale capture. `_ExampleSeedState.start()` holds
`self._lock` while it sets `_last_error = None` and calls `thread.start()`. The
seed thread fails immediately and blocks on that same lock; the handler then calls
`last_error()`, which also wants it. Whoever wins decides whether `error` is `null`
or a string. The suite observes this route's `[ok]` POST **exactly once**, right at
that moment.

So the frozen entry recorded a scheduler outcome and published it as an API
contract. On Linux/CI the thread wins and the gate is green; on macOS the caller
wins (measured 0/600 the other way, even at a 1µs switch interval) and every macOS
developer got a `BREAKING` report on a file nobody had touched.

### Fixed with a test, not by editing the artifact

The file's stated claim is that it was captured from real responses. Hand-editing
the entry would trade a wrong shape for a wrong provenance — the worse failure,
because provenance gets believed.

The new test drives the **already-seeded** POST path, which `docs/webapp-api.md`
documents ("Idempotent: already seeded → `{seeded: true, started: false}`") and
which nothing exercised. There `existing is not None` short-circuits before
`start()`, so `error` and `frame_id` pass through deterministically. Two
observations — one with an error recorded, one on a runner that never failed —
pin both halves of both fields regardless of who wins the race. The seeded state is
a **real store row** written the way the seeder writes it, not a patched lookup, so
the recorder stays on and the published shape stays honest.

Regenerated: 3 type changes; 796 shapes and 151/151 coverage unchanged.
`["null","string"]` is a superset of both race outcomes, so the entry now admits
either machine instead of calling one of them a breaking change.

### A survey, because this one is not alone

94 fields across 43 route entries are frozen as `null`-**only** — a type nothing
can legitimately have unless it is a constant null. `frame_id` on both
`/example/session` verbs was two of them (fixed here). The rest — e.g.
`GET /frames[].model`, `GET /frames/…/plan.plan_id`, `PATCH /me.email` — are latent
versions of the same thing, waiting for the first capture that sees the populated
state.

A note in `response_capture.py` records this and distinguishes it from
`_MACHINE_STATE_KEYS`. The tempting fix for the other 90 is to elide them there;
that would delete real guarantees to silence a coverage gap. They are
**under-observed**, not host-dependent, and each wants a test that reaches the
other state.

## Area

- [ ] Web UI / frontend
- [ ] Agent / loop / delegation
- [ ] Kernel / host RPC / runtime
- [x] Server / gateway / API
- [ ] Store / provenance / artifacts
- [ ] Skills / science runtime
- [ ] Compute / remote execution
- [ ] CLI / config / packaging
- [x] Tests / harness / CI
- [ ] Docs

## Change Type

- [x] Bug fix
- [ ] Feature
- [ ] Refactor
- [x] Test / harness
- [ ] Documentation
- [ ] Security-related change
- [ ] Release / packaging

## Verification

Ran:

```text
uv run python scripts/capture_response_schemas.py --check
  -> no breaking change; 796 route/status shapes; coverage 151/151

uv run pytest                      # full offline suite via the --check run above
uv run pytest tests/test_gateway.py -k example_seed
uv run pre-commit run --all-files  # clean

Determinism: the capture was repeated 5x and POST /example/session [ok] came back
["null","string"] for both `error` and `frame_id` every time. Before the fix the
same repetition gave `null` 12/12 on macOS while CI froze `string`.

Attribution: the drift was confirmed pre-existing by checking out the base
commit's version of the changed files and re-running the gate with conditions
held constant — same failure, so it was not caused by any concurrent work.

Verified again after rebasing onto current main (which moved host_dispatch.py and
store.py underneath a *captured* artifact): --check still clean, 796 / 151-of-151.
```

Not run:

```text
The Linux/py3.12 capture, i.e. the machine whose scheduling produced the original
`string`.
```

Reason:

```text
No Linux host here. The claim that the union holds on both is structural rather
than observed: `check_compatible` passes whenever the observed type set is a
subset of the frozen one, and ["null","string"] is a superset of both race
outcomes. CI on this PR is the actual proof, and it is the one place that can be.
```

## Risk and Reviewer Focus

Low blast radius: one new test, one comment block, and three type widenings in a
generated artifact. No production code path changes.

Look first at:

- The artifact diff. It should be exactly three `"type"` entries on the two
  `/example/session` rows and nothing else. If it is broader, the regeneration
  picked up something host-specific and should not be merged.
- The new test's use of a real `store.new_frame` + `update_frame` rather than a
  patched `_example_session_frame`. That is deliberate: a stub would have to carry
  the `stubbed_backend` marker, which pauses the recorder, which would defeat the
  point of the test.
- Whether the widened entry is the contract you want published. It says `error`
  and `frame_id` are nullable on both verbs, which matches the source.

Note `fix/byoc-confinement-probe-and-docs` independently arrived at
`error: ["null","string"]` via a re-capture. Corroborating, but that branch's
`frame_id` is still `null` on both verbs and it has no test forcing the seeded
state — so it is another lucky capture rather than a fix. Merge order does not
matter; this PR is what keeps it from regressing.

## Checklist

### Diff Readiness

- [x] I reviewed and understand the full diff.
- [x] This PR is small and single-purpose.
- [x] No unrelated formatting, broad rewrite, or drive-by refactor is included.
- [x] Hotspot files were edited surgically if touched: none of the hotspot files
      are touched by this PR.
- [x] `openai4s/server/webui/vendor/` and `tests/fixtures/` were not reformatted.

### Tests

- [x] Relevant tests or manual checks were run and listed above.
- [x] No new test requires live LLM, network, GPU, SSH, Docker, lab hardware, or
      secrets in the default offline suite.
- [x] No tests were deleted without tracked replacements.
- [x] Kernel / host-RPC / gateway changes include focused contract coverage or a
      documented smoke test. (This PR *is* contract coverage for a gateway route.)

### Core Dependency Policy

- [x] No hard third-party import was added to the core engine, LLM client, or
      stdlib web server.
- [x] Optional science imports are guarded by `try/except ImportError` at every
      in-tree use site. (None added.)
- [x] New dependencies, if any, are documented and justified. (None.)

### Public Disclosure and Security

- [x] No secrets, API keys, tokens, real credentials, private data, model
      weights, or local absolute paths are included.
- [x] No unpublished research roadmap, internal assignment, benchmark detail, or
      unreleased experimental result is disclosed.
- [x] Security-sensitive changes include appropriate synthetic tests or manual
      verification notes. (Not security-sensitive.)
- [x] Docs do not overstate isolation, sandboxing, privacy, or security
      guarantees.

### Docs

- [x] Docs match actual code behavior. The published contract now matches what
      the route returns, which is the entire point of the change.
- [x] User-facing behavior changes are reflected in docs or release notes where
      appropriate. (No behavior change; `docs/webapp-api.md` already described the
      idempotent path this now tests.)
- [x] `README.md` and `README_zh.md` stay in sync where translated sections are
      affected. (Not affected.)

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `addc2f52cb2b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.