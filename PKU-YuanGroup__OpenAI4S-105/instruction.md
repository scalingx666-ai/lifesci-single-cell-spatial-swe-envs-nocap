# Issue

**Title:** refactor(http): one bounded body reader, and what the second defense hid

## Description

## Summary

Stacked on #96, targeting its branch so the diff under review is only the
structural pass. #96's diagnosis and behaviour are right — a fully-read
response really did die on its own closed socket, and this branch does not
change that outcome. What it changes is the shape.

The fix landed as **two mechanisms, either of which is sufficient on its own**:
the readers stop at `response_body_exhausted`, *and* `socket_timeout_setter`
returns a wrapper that swallows `settimeout` on a retired socket. Ablation over
a real socketpair on 3.13:

```text
only response_body_exhausted  -> passes
only the settimeout wrapper   -> passes
neither                       -> Doubao search request failed (OSError)
both (as merged in #96)       -> passes
```

Two answers to one question is a place for them to disagree, and the wrapper
carried a trap only a comment guarded: consult `_closed` instead of `fileno()`
and every `Connection: close` body silently loses its read bound — invisible to
every fixture here, because a socketpair payload never has to wait. So the
wrapper is gone and `socket_timeout_setter` returns the bound `settimeout`
again. The stop condition moved to the top of the loop, where testing
exhaustion *before* arming is what makes the retired socket unreachable rather
than something a tolerant setter has to absorb.

The two capped readers were the same forty lines, and the earlier
`read1`/slow-drip fix had already been written into each by hand. They are now
`http_deadline.read_body_capped(...)`; each consumer is only its own failure
vocabulary. Consolidating surfaced three things one copy knew and the other did
not:

- **An empty read was accepted as a complete body.** A peer declaring
  `Content-Length: 99` that sends 59 and closes returned 59 bytes with no
  error, and the boundary diagnosed the cut connection as invalid JSON.
- **`_read_body` accepted a missing read bound in silence** where its twin
  called the identical state fatal. Fatal for both now; Doubao keeps its
  escape hatch for an injected test opener.
- **The exhaustion signals were matched loosely.** `bool(is_closed())` calls a
  `Mock`'s auto-attribute end-of-body, and `length == 0` is equally true of
  `False`. Both truncate a body after one chunk.

`_socket_retired` survives with exactly one caller, `register_response` — and
it is *not* the old second defense. `remaining()` proving the budget intact
does not keep it intact; the bare `OSError` that escaped when the watchdog won
that gap left `__exit__` with `exc_type` set, so an abort was reported as
`... failed (OSError)` instead of the deadline. Reproduced, and now pinned.

Also here: the `fp`/`raw`/`_sock` walk is one lazy generator shared by the
setter and the watchdog lookup; the end-of-body accessors resolve once per
response instead of once per chunk; and the socketpair fixture no longer leaks
its descriptors when setup raises.

Size, honestly: `openai4s/` is **+269/-151** raw lines against #96, but that is
docstrings — the executable statement count across the three modules goes
**892 -> 870**, i.e. **-22 statements** while covering three failures #96 did
not. The prose grew because the reasoning that used to be spread across two
copies of the loop is now stated once, next to the loop.

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

Same caveat as #96: no box names it exactly. The change is in the shared
outbound stdlib HTTP transport (`http_deadline.py`) and its two consumers. No
route, serializer, or response shape was touched.

## Change Type

- [x] Bug fix
- [ ] Feature
- [x] Refactor
- [x] Test / harness
- [ ] Documentation
- [ ] Security-related change
- [ ] Release / packaging

## Verification

Ran:

```text
uv run pytest                                          # 5146 collected, 0 failures
uv run pytest tests/test_doubao_search.py tests/test_mcp_client.py tests/test_egress_surface.py
                                                       # 68 passed on 3.13 and on the 3.10 floor
uv run mypy                                            # clean
uv run python -m harness.cli run --tier pr --offline   # 15/15
uv run python scripts/check_directory_readmes.py       # complete bilingual coverage
python scripts/source_secret_scan.py                   # passed (1134 files)
pre-commit isort / black / ruff / mypy-core            # all Passed (commit hook)

ablation: delete the single stop condition
  -> all three of #96's new tests go red; nothing else covers for it
mutation: _socket_retired consults _closed
  -> test_a_socket_urllib_already_closed_still_takes_its_read_bound goes red
mutation: register_response arms with a bare sock.settimeout(...)
  -> test_a_watchdog_close_is_reported_as_the_deadline_not_as_a_bare_oserror
     goes red with OSError: [Errno 9]

one live request through each real consumer, isolated temp Store, no daemon:
  Doubao Search  -> available=true, source=doubao, count=5
  DataPro MCP    -> tools/list answered
  both fail with (OSError) on 1579b6f^ and succeed on this branch
```

Not run:

```text
scripts/capture_response_schemas.py --check
scripts/capture_response_contract.py --check
scripts/container_smoke.sh
tests/browser_smoke.mjs / browser_admission_fault.mjs / browser_matrix.mjs
```

Reason:

```text
No gateway route, serializer, or response envelope changed, so neither frozen
response contract can move. Docker and Playwright were unavailable in the
environment this was prepared in; CI runs all four jobs.
```

## Risk and Reviewer Focus

Read these three together — they are the whole judgement call:

1. **`socket_timeout_setter` no longer tolerates a retired socket.** That is
   safe only because `read_body_capped` tests exhaustion at the *top* of the
   loop, so no arming ever follows the stdlib's end-of-body close: a known
   `Content-Length` exits on the exhaustion test, chunked and close-delimited
   bodies exit on the read that returns `b""`. If you move that test back below
   the read, restore the wrapper with it.
2. **`_socket_retired` still tests `fileno() < 0` only, and must not consult
   `_closed`.** urllib closes the connection socket while `makefile` holds an
   I/O reference, so `_closed` is true for the whole body.
   `test_a_socket_urllib_already_closed_still_takes_its_read_bound` is that
   invariant as a test rather than a comment.
3. **`on_unbounded` makes a missing read bound fatal for MCP too.** Verified
   against the live endpoint that a production response always carries a
   reachable socket. The MCP response double in the test file gained the
   transport it was missing — a fake with no socket beneath it is not a cheaper
   HTTP response, it is a state the real transport never produces.

Two knock-on edits worth a glance: `import time` became dead in both consumers,
so the slow-drip test's `monkeypatch.setattr(mcp_http.time, ...)` moved to
`http_deadline.time`, which is where the budget is consulted now.

Deliberately **not** done: `tests/test_mcp_client.py`'s `_EndOfBodyClosingResponse`
re-models the same 3.11+ retirement as the double in `tests/test_doubao_search.py`.
With the reader shared, one socketpair test on the helper covers that contract
and this double is surplus — but deleting a test #96 added is the author's call.

## Checklist

### Diff Readiness

- [x] I reviewed and understand the full diff.
- [x] This PR is small and single-purpose.
- [x] No unrelated formatting, broad rewrite, or drive-by refactor is included.
- [x] Hotspot files were edited surgically if touched: none of `gateway.py`,
      `host_dispatch.py`, `store.py`, `app.js`, `worker.py`, `manager.py` is
      touched.
- [x] `openai4s/server/webui/vendor/` and `tests/fixtures/` were not
      reformatted.

### Tests

- [x] Relevant tests or manual checks were run and listed above.
- [x] No new test requires live LLM, network, GPU, SSH, Docker, lab hardware,
      or secrets in the default offline suite. The new socket tests use a local
      `socketpair`; the live requests above are manual and outside the suite.
- [x] No tests were deleted without tracked replacements. One test added on top
      of #96 during review was replaced by two real-socket tests covering the
      same guard more directly; #96's own tests are all retained and all still
      fail against its parent.
- [x] Kernel / host-RPC / gateway changes include focused contract coverage or
      a documented smoke test.

### Core Dependency Policy

- [x] No hard third-party import was added to the core engine, LLM client, or
      stdlib web server.
- [x] Optional science imports are guarded by `try/except ImportError` at every
      in-tree use site.
- [x] New dependencies, if any, are documented and justified: none added.

### Public Disclosure and Security

- [x] No secrets, API keys, tokens, real credentials, private data, model
      weights, or local absolute paths are included.
- [x] No unpublished research roadmap, internal assignment, benchmark detail,
      or unreleased experimental result is disclosed.
- [x] Security-sensitive changes include appropriate synthetic tests or manual
      verification notes.
- [x] Docs do not overstate isolation, sandboxing, privacy, or security
      guarantees.

### Docs

- [x] Docs match actual code behavior: no documented behaviour changes, the
      reasoning lives in the touched docstrings.
- [x] User-facing behavior changes are reflected in docs or release notes where
      appropriate.
- [x] `README.md` and `README_zh.md` stay in sync where translated sections are
      affected: no translated section is affected.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1579b6fb4de2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.