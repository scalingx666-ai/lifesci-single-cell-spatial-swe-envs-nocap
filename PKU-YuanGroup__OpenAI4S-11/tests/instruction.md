# Issue

**Title:** fix(security): resolve open CodeQL code-scanning alerts

## Description

## Summary

Resolves the open **CodeQL code-scanning alerts** on `main` (24 open: #1–#11, #13–#25; #12 was already fixed). Each alert class is addressed in its own commit; all fixes are surgical and behaviour-preserving.

| Area | Alerts | Fix |
| --- | --- | --- |
| `openai4s/jobs.py` | #14 `py/path-injection` | Confine a request-supplied job `cwd` under the jobs root via `Path.relative_to`; escapes are rejected, not created. |
| `openai4s/server/gateway.py` | #11 `py/http-response-splitting` | `_sanitize_header_value()` strips CR/LF (+C0 control) from the Content-Type and every `extra` header in `_send()`. |
| `openai4s/server/gateway.py` | #15/#16/#17 `py/path-injection` | `/static/` reject absolute/`..` on the raw path, then confine the resolved target with `Path.relative_to` (also backstops symlinks). |
| `openai4s/server/webui/app.js` | #19/#20 `js/client-side-unvalidated-url-redirection`, `js/xss` | `safeUrl()` allowlists http(s)/mailto before a search-result URL is used as an `href`. |
| `openai4s/server/webui/app.js` | #21 `js/xss` | `kvRow` branches on `instanceof Node`; untrusted strings go to `textContent`, never `appendChild`. |
| `openai4s/server/webui/app.js` | #22 `js/request-forgery` | `encodeURIComponent` the WS `frame_id`; `api()` requires a same-origin, single-leading-slash path. |
| `openai4s/server/webui/app.js` | #24 `js/prototype-polluting-assignment` | `S.permCards` is `Object.create(null)`; read-then-write sites guard with `hasOwnProperty`. |
| `openai4s/server/webui/app.js` | #18 `js/redos`, #25 `js/regex-injection` | `renderMd` table-delimiter matched cell-by-cell (no nested quantifier); closing fence detected by a plain scan (no dynamic `RegExp`). |
| `skills/literature-review/kernel.py` | #13 `py/redos` | Ambiguous DOI-strip regex → equivalent, linear `str.rstrip`. |
| `tests/test_egress.py`, `tests/test_webtools.py` | #1–#10 `py/incomplete-url-substring-sanitization` | Substring URL checks → exact message equality / set-subset / `urlparse().hostname` (equivalent or stricter). |

**Not in this PR — #23 `js/functionality-from-untrusted-source`** (`tests/fixtures/arxiv_abs_2503.06687.html:37`, CDN script with no SRI). This is a **byte-exact captured third-party HTML fixture** (pre-commit excludes `tests/fixtures/`); editing it would defeat its purpose. It is dismissed as a won't-fix/false-positive in the code-scanning UI rather than modified.

Each fix was adversarially reviewed (independent per-alert verification of sink neutralisation + regression + bypass search) before commit; the gateway `/static/` fix was hardened from `.parents` to the CodeQL-recognised `relative_to` on that review's feedback.

## Area

- [x] Web UI / frontend
- [ ] Agent / loop / delegation
- [ ] Kernel / host RPC / runtime
- [x] Server / gateway / API
- [ ] Store / provenance / artifacts
- [x] Skills / science runtime
- [x] Compute / remote execution
- [ ] CLI / config / packaging
- [x] Tests / harness / CI
- [ ] Docs

## Change Type

- [x] Bug fix
- [x] Security-related change

## Verification

Ran:

```text
uv run pytest                          # 299 passed (offline; no network, no secrets)
uv run pre-commit run --all-files      # black · isort · ruff · hygiene — all pass
uv run python -m compileall -q openai4s openai4s_compute_provider tests skills

# Live gateway smoke test (fresh temp data dir):
#   GET /static/app.js, /static/style.css, /static/vendor/3Dmol-min.js  -> 200
#   GET /static/../../server/gateway.py (--path-as-is)                   -> 403
#   GET /static//etc/hosts                                              -> 403
#   POST /api/compute/jobs {"cwd":"/tmp/pwn"}         -> {"error":"cwd escapes the jobs root"} (dir NOT created)
#   POST /api/compute/jobs {"cwd":"../../../../tmp/pwn2"} -> rejected
#   Response headers verified free of injected CR/LF.

# Behaviour equivalence, in isolation:
#   renderMd table-delimiter + fence helpers (incl. the former ReDoS input -> 0 ms)
#   DOI rstrip == old regex over edge cases (0.001 ms on 200k chars)
#   node --check openai4s/server/webui/app.js
```

Not run:

```text
Full in-browser WebSocket end-to-end of the UI changes.
```

Reason:

```text
The JS changes are localised, defensive, and behaviour-preserving (verified via node syntax/logic
harnesses and, for the server side, live curl). There is no JS test suite in-tree (the web UI is
static, served from the tree; the pytest suite is Python-only). The touched paths degrade safely:
non-http(s) links render as text, permission-card keys are unchanged for normal ids, and encodeURIComponent
is a no-op for hex/uuid frame ids.
```

### PR checklist

- [x] Offline tests pass with no network and no secrets.
- [x] Lint/format passes.
- [x] No hard third-party import added to the core.
- [x] No secrets/keys/tokens in code, tests, fixtures, logs, or docs.
- [x] Hotspot files (`gateway.py`, `app.js`) edited **surgically**, not rewritten.
- [x] `webui/vendor/` and `tests/fixtures/` not reformatted.
- [x] No tests deleted (`git ls-files --deleted` clean); test assertions tightened, not removed.

### Files that most need human review

- `openai4s/server/webui/app.js` — the `safeUrl`, `api()` guard, `permCards` null-proto, and `renderMd` regex rewrites (no JS test coverage).
- `openai4s/server/gateway.py` — `_serve_static` containment and `_send` header sanitisation.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6048ad91ed4c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.