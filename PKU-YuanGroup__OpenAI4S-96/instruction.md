# Issue

**Title:** fix(doubao,mcp): a fully-read response died on its own closed socket

## Description

## Summary

Doubao Search failed with `Doubao search request failed (OSError)` *after* the
upstream answered HTTP 200 and the reader had consumed every result byte.

`HTTPResponse.read1` retires the transport on the same call that returns the
final byte of a known `Content-Length` (CPython 3.11+; only the 3.10 floor waits
for one further empty read), and urllib closed the connection socket back when
the headers arrived, so that last read drops the remaining `makefile` I/O
reference and the descriptor goes away. Both capped body readers re-armed the
socket read timeout at the top of every pass, so arming it once more after the
last chunk raised `OSError` (EBADF), and the controlled boundary projected a
finished exchange as a failed request. `mcp_http.py::_read_body` is the same
loop and failed the same way for any MCP HTTP reply carrying a `Content-Length`.

This was not a race: it was every such response on every interpreter above the
3.10 floor. It stayed invisible because the development venv is 3.10 — the one
version that waits — and every offline test used a `BytesIO` fake with no socket
underneath, and nothing under those refuses a `settimeout`.

A reader now stops when the body is exhausted, and the timeout setter skips a
socket whose descriptor is already gone while still raising for a live one. A
closed socket cannot block, so it needs no bound; a live one must keep its
bound, so the slow-drip protection is unchanged.

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

No box names it exactly: the change is in the shared outbound stdlib HTTP
transport (`http_deadline.py`) and its two consumers, the Doubao Search client
and the MCP HTTP client. No route, serializer, or response shape was touched.

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
uv run pytest tests/test_doubao_search.py tests/test_mcp_client.py tests/test_egress_surface.py   # 66 passed
uv run pytest tests/test_doubao_search.py tests/test_mcp_client.py   # on 3.12 and on 3.13: 56 passed each
uv run mypy                                            # clean
uv run python scripts/check_directory_readmes.py       # complete bilingual coverage
uv run python -m harness.cli run --tier pr --offline   # 15/15
pre-commit isort / black / ruff / mypy-core            # all Passed (commit hook)
uv run pytest                                          # see note below
each new test, re-run with the source change reverted   # every one fails, on 3.10 and on 3.13
one live request to the provider through a local daemon's own /doubao-search/search route
  # available=true, source=doubao, count=8 (before the change: the OSError above)
```

The full offline suite reports 25 failures in this environment, byte-identical
to a clean tree: no local R runtime, and Seatbelt plus outbound TLS restricted.
None are in the touched modules.

Not run:

```text
scripts/capture_response_schemas.py --check
scripts/capture_response_contract.py --check
scripts/container_smoke.sh
tests/browser_smoke.mjs / browser_admission_fault.mjs / browser_matrix.mjs
```

Reason:

```text
No gateway route, serializer, or response envelope changed, so the two frozen
response contracts cannot move. Docker and Playwright were unavailable in the
environment this was prepared in; CI runs all four jobs.
```

## Risk and Reviewer Focus

Both changes bear on whether a body read stays bounded, so read them together:

1. `http_deadline.socket_timeout_setter` now returns a wrapper rather than the
   bound `settimeout`. `_socket_retired` deliberately tests `fileno() < 0` only.
   It must **not** consult `_closed`: urllib calls `sock.close()` while
   `makefile` still holds an I/O reference, so `_closed` is true for the whole
   body and treating it as retired would silently drop the read bound for every
   response. The `except OSError` path re-raises unless the socket is retired,
   so a live transport that refuses a timeout is still a hard failure.
2. `response_body_exhausted` returns on `isclosed()` or a remaining `length` of
   zero. Both are end-of-body, not error states; the second is what the 3.10
   floor reports one read earlier. A reader stopping there returns the same
   bytes and skips only a read that would have returned `b""`.

The new deterministic fake in `tests/test_doubao_search.py` is the contract
worth reviewing: it models the stdlib behaviour so the 3.10 CI job fails on this
too, rather than passing because its interpreter is the immune one.

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
      or secrets in the default offline suite. The new socket test uses a local
      `socketpair`, and the network-policy calls around it are patched out so no
      DNS lookup or connection leaves the process.
- [x] No tests were deleted without tracked replacements.
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

Made with [Cursor](https://cursor.com)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fe2187019c35`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.