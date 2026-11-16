# Issue

**Title:** fix(file): bound read_file and take it off the event loop

## Description

Agent-side half of the large-file problem. Frontend half is .

## What happened

Opening a 100 MB file in the UI's file panel made the agent stop answering NATS health checks, and the Hub recycled the whole sandbox. Staging, 2026-08-04:

```
00:55:07  Pod admin_001 health check timeout
00:55:40  Pod admin_001 health check timeout
00:56:03  Creating Modal Sandbox   ← Hub gave up on the agent
```

## Cause

`read_file` did this:

```python
with open(target_path, "r", encoding="utf-8") as f:
    lines = f.readlines()
```

Synchronous, unbounded, **on the event loop thread**, and — the part that makes the existing guards useless — *before* any limit is applied. `max_file_read_lines`, `max_file_read_chars` and `start_line`/`end_line` all filter a list that has already been fully materialised.

So a 100 MB file became one multi-hundred-megabyte string inline. NUL bytes are valid UTF-8, so a binary didn't even fail fast on decode — it sailed through and became 100M characters.

Request dispatch was never the problem: `NATSRemoteWorker._handle_request` already spawns each request with `asyncio.create_task`. The **event loop itself** was blocked, which is why even `_ping` — whose handler is documented as *"Must not block"* — couldn't answer.

## Fix

The read is bounded at `MAX_READ_CHARS` and runs via `asyncio.to_thread`, so neither the file I/O nor the UTF-8 decode touches the event loop.

Past the ceiling the caller still gets the file's head, marked `truncated`, with a hint to page via `start_line`/`end_line` or stream with `open_file_for_read` + `read_chunk_at`. That's more useful than a bare error for the common *"show me the top of this log"* case. Files under the ceiling behave exactly as before.

Detecting the overflow costs one extra character, not another pass over the file:

```python
data = f.read(max_chars)
truncated_by_size = f.read(1) != ""
```

## Tests

5 new tests: the ceiling cuts and reports it, small files read whole and untruncated, line endings survive the split (`read_file` joins them back), a huge file returns promptly marked truncated, and normal files are unaffected.

`tests/test_file_manager.py` + `tests/test_file_manager_broken_symlink.py`: 17 passed, 1 skipped on this branch. The 2 pre-existing failures in `test_think_plugin.py` fail on `main` too and are unrelated.

## Why both halves

pantheon-ui#29 stops the file panel from requesting an unbounded read. This makes the agent resilient when something still does — a user running `cat` on a big file by hand, a skill that reads a BAM, anything not routed through the panel.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c15440df1633`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.