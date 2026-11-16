# Issue

**Title:** feat(desktop): let the agent author apps — desktop_open(module=…) + skill

## Description

## What

Closes the "agent can drive apps but can't ergonomically **build** one" gap. The architecture already lets an agent install a workspace app by writing files (workspace scope is "the agent, automatically"), but the fast ephemeral path was retired-and-excluded (`open_live_view`) and no skill taught authoring. **live_view stays retired** — this routes everything through the current `desktop.*` surface.

## Pod (this PR)

- **`desktop_open(module=…, title=…)`** — pass a frontend ES-module SOURCE (`export function setup(app, root){…}`) and it opens as a **bespoke window**: no manifest, no install, drivable by `desktop_read/update/set/call` like any packaged app. The pod writes it under `.pantheon/bespoke/`, serves it via the data server, and emits `desktop.open` with the `module_url`. This replaces `open_live_view`'s custom path (which stays `@tool(exclude=True)`).
- **desktop skill → "Building your own app"** — path A (bespoke `desktop_open(module=…)`) and path B (a package under `.pantheon/apps/<id>/`, where a file write *is* the install), with the `setup(app,root)` bridge contract and a minimal `atrium.json`.
- **`live-view-app.md` marked DEPRECATED**, pointing at the desktop skill; the `setup()` contract is preserved in a `<details>` block.

## Shell (companion, in pantheon-atrium, already merged)

- Bespoke open: `desktop.open` with `module_url` → `agent-view` window under the same WindowBridge.
- **Re-discover on miss**: `desktop_open` of an unknown id re-scans `.pantheon/apps` once before erroring — a just-written app opens without a reconnect.
- **Init-state race fix**: the app-host's boot-time `init` could lose the race against module load (confirmed: iframe `onState` never fired while the shell cache held the state); the bespoke branch re-pushes open-state once the window is READY.

## Verification

Headless against a live staging pod: author a `setup(app,root)` module (both `.js` and `.jsx`/Sucrase), open it, drive it — `desktop_call` runs the action, initial state arrives (n=5 → bump → 6), `desktop_read` round-trips. Full agent-in-chat e2e after this image builds + deploys.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `de0a2aaf9269`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.