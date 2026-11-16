# Issue

**Title:** feat(endpoint): app backend supervisor — one process per Atrium app

## Description

The Atrium app runtime's cut 2, endpoint half (pantheon-atrium `docs/app-spec.md`, frozen v1 §5–§6). An installed Atrium app may ship a Python backend; it runs in **its own subprocess**, spawned lazily and supervised by the project endpoint. The endpoint runs no app code — nothing an app does can take down routing, the file panel, or another app. Same ladder as ChatRoom spawning the endpoint and the Python toolset moving user code into a Jupyter kernel: the failure domain moves, the state does not.

## What's in it

- **`pantheon/endpoint/apps.py`** — `AppSupervisor`: scans the install scopes (`<workspace>/.pantheon/apps` → `~/.pantheon/apps` → factory templates, first per id), spawns backends lazily, speaks line-delimited JSON-RPC over the child's stdio, reaps idle processes (10 min), backs off on crashes ([1,2,4,8,16]s, 5 tries, then parked with the stderr tail as the reason).
- **`pantheon/endpoint/app_runtime.py`** — the child bootstrap. **Stdlib-only, by path, deliberately**: the interpreter comes from the manifest (`caps.python.env`, resolved against the conda env roots) and a conda analysis env has no `pantheon` package to import. Imports the app's `backend/`, runs `register(ctx)`, serves the pipe. `AppContext` = `workspace` / `@method` / `serve()` (answered by the endpoint's live_view data server) / `state` (JSON KV under `.pantheon/app-state/<id>/`, outside the package dir so resync and uninstall cannot eat it) / `log`.
- **`core.py`** — two new tools: `app_call(app_id, method, args, timeout_s)` (the dispatch; refuses methods the handshake never registered — `unknown method` comes from the registration table, never from a timeout) and `app_registry()` (rescans on every call; an install is a file write and a cached registry is how it goes stale).

## The registration mechanism

scan → REGISTERED entries before any process exists; handshake → the methods `register(ctx)` collected become the entry's callable surface; dispatch → refusal from the table; lifecycle → `registered → spawning → ready → reaped`, or `crashed(n) → failed`.

## Verification

Smoke-tested end to end without a pod (child and supervisor halves, stub endpoint): handshake + method registration, invoke with interleaved `ctx.log`, `ctx.serve` round trip, error crossing, dispatch-table refusal, clean shutdown, state surviving restart, and `kill -9` → backoff → respawn. First real consumer is Atrium's packaged Viv (`apps/viv/backend/` — the OME conversion moving out of the shell), already merged on the Atrium side and gated on this landing.

No behaviour change for anything that does not call the two new tools.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01Ups1TP9FXNqxbaaUXuEDrn

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `95e17eb39e36`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.