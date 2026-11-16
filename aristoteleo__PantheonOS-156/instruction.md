# Issue

**Title:** feat(toolsets): pty — a real terminal in the sandbox

## Description

## Why

`shell` runs commands behind pipes with an end-of-command marker. That is the right shape for an agent — one command, its complete output — but it is not a terminal. With no tty, bash never enters readline, so a UI gets no prompt, no tab completion, no job control, and cannot run `vim`, `top` or `less` at all. Output also only arrives once the command finishes.

This adds `PtyToolSet`: a pseudo-terminal with a shell running on it in its own session, so the shell is that pty's controlling process and Ctrl-C reaches the foreground job rather than the agent. Output streams as it is produced on the NATS stream `pty_<session_id>`, which a frontend subscribes to directly.

Written for Pantheon Atrium (a desktop frontend), but nothing in it is Atrium-specific — any UI wanting a terminal can use it.

## Surface

All `@tool(exclude=True)` — an agent has no use for a byte stream it would have to render.

| | |
|---|---|
| `pty_open(cols, rows, cwd, shell)` | → `session_id`, `stream_id` |
| `pty_write(session_id, data)` | base64 keystrokes, control chars included |
| `pty_resize(session_id, cols, rows)` | TIOCSWINSZ + SIGWINCH |
| `pty_close(session_id)` | |
| `pty_list()` | |

Bytes are base64 in both directions: a pty carries arbitrary bytes, and a UTF-8 sequence split across two reads is ordinary — JSON cannot hold it.

## The one design decision worth reviewing

The pty is watched by the event loop (`add_reader`), **not** by a blocking read in `run_in_executor(None, ...)`.

The threaded version is the obvious one, and it is what I wrote first. It costs one default-executor worker for the entire life of the session — and `PythonInterpreterToolSet` submits every `run_python_code` call to that same pool. A few open terminals would throttle, and eventually starve, code execution.

Reads land in a per-session `asyncio.Queue` and a single task publishes from it. Publishing straight from the reader callback would mean a task per read, and tasks complete in whatever order the network allows; a terminal whose output arrives out of order is worse than one that arrives late. A burst drains into one message rather than dozens.

## Verification

Nine checks locally against a real pty:

- `tty` reports a real device, `test -t 0` is true
- `$COLUMNS` follows both the initial size and a resize
- Ctrl-C interrupts a running `sleep 30`; the shell survives
- 400 lines of burst output arrive complete and in order, coalesced into ~150 messages
- no executor thread is held (2 threads alive)
- `pty.exit` is published both when the shell quits itself (`exit 7` → code 7) and on a deliberate close (−1, SIGHUP)
- no session or fd is left behind either way
- calls against a dead or unknown session return errors rather than raising

## Deployment

Merging builds `nanguage/pantheon-agents:latest` via `docker-build.yml`, which is what **staging** tracks. `:prod` is pinned separately and only moves through `promote-agent.yml`, run manually — **this PR does not touch production.**

Two notes for review:

- `pty` is not in `builtin_services`; it auto-starts lazily on first `proxy_toolset` call, so it costs a cold sandbox nothing.
- `_prepare_toolset_args` now passes `workdir` for `pty` as it does for `shell`/`python_interpreter`, so a terminal opens in the workspace rather than wherever the agent's cwd happens to be.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01BhPiGNfkhLZ89Sqhoz9ebP

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3a54f06ddb5b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.