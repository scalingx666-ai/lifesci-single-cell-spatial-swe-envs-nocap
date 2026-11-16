# Issue

**Title:** feat: multi-project backend — local TCP transport, per-project endpoints + memory

## Description

Run multiple project folders concurrently in the web version (replaces the old "one project, blocked while a task runs" model).

## What's in here
- **Local TCP remote backend** for ChatRoom↔Endpoint RPC (avoids cross-public NATS round-trips); dual-channel endpoint serves ChatRoom over TCP and the frontend over NATS on the same service id.
- **Per-project endpoints**: lazily spawn one endpoint subprocess per project (process isolation solves the global `os.chdir`/`Settings` singleton problem); route chats / agents / teams by the chat's project. Per-project spawn is serialized with a lock.
- **Per-project memory** (`ProjectRoutedMemoryManager`): each chat's memory lives in its own project's `.pantheon/memory`; per-chat ops route to that store (concurrency-safe), list/new target the active project. Active project never null (falls back to the work-dir "home").
- **Lightweight `set_active_project`** (no chdir / no settings·memory·template singleton reset) so switching the viewed project doesn't interrupt running tasks; `list_running_chats` reports running work across all projects.

Tested end-to-end (TCP backend, per-project endpoints, memory routing, running indicators) via headless Playwright + Python.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c605b7441100`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.