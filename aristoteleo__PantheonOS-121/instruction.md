# Issue

**Title:** feat(chatroom): multi-window backend — real per-project endpoints in bundle + store-based chat listing

## Description

Backend support for the pantheon-desktop multi-window feature (one window per project, one shared backend).

- **routed_memory**: `new_memory_in` / `list_all_memory_metadata` / `list_memory_metadata_in` for per-project (per-window) chat stores.
- **room.list_chats**: list a registered project's store directly — chats live in a store, not reliably tagged with `project.name`, so a name filter hid them.
- **room._spawn_project_endpoint**: when frozen (PyInstaller), spawn via the chatroom exe's `endpoint` subcommand. `-m pantheon.endpoint` does not work in a frozen binary → it fell through to `start_services` (a misrouted chatroom that opened a browser + exposed the wrong work dir). + `PANTHEON_DISABLE_AUTO_UI` kill-switch.
- **chatroom/__main__**: add `endpoint` subcommand routing to `start_endpoint`.

Pairs with pantheon-ui `feat/desktop-multi-window`. Verified end-to-end on the bundled macOS app.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a7bb77645b24`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.