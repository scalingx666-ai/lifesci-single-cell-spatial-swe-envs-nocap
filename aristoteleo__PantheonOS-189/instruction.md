# Issue

**Title:** feat(desktop): the pod owns the window session

## Description

## Why

Three desktops open on one pod showed three different sets of windows. Each viewport kept its own window list and wrote the whole thing to `.pantheon/desktop.json` on a debounce, reading it back only at boot and only onto an empty desktop — **two writers to one file with no reader between them**. They took turns overwriting each other and neither ever saw the result.

A desktop is not a page: it is a view onto the pod, which already owns the files, the processes and the installed apps. Which windows are open is a property of the machine.

## What

- `desktop_session.py` — the document, and a reducer that is a pure function of it. Clients send **intents**; every change bumps `seq` and emits ops.
- `desktop_intent` / `desktop_session_get` (UI-only) — apply-and-broadcast, and the snapshot a viewport attaches or re-syncs with. The intent reply carries its own ops so the caller can render immediately; applying by `seq` makes the broadcast idempotent.
- **Pod-scoped stream** (`<prefix>.pantheon.stream.desktop`), not per chat. Tying desktop events to a conversation is what produced *"the desktop did not answer — is an Atrium window open on this chat?"*, and it left the standalone desktop page — which has no chat — unable to participate.
- **Ids are minted pod-side.** A per-tab counter gave every copy its own `win-3`.
- `desktop_windows` is answered from the document, so it needs no browser.

Not shared, deliberately: the space a viewport is looking at, and keyboard focus. Those belong to the person; stacking order belongs to the arrangement.

## Verification

The reducer was exercised standalone (no pod): intents, pod-minted ids, space collapse, grow-only resolution, unknown-intent and missing-window errors, and a v1 record migrating rather than being dropped at upgrade.

That last test caught a real bug before it shipped: `to_record` wrote windows without their ids while `from_record` keyed on them, so **every window would have vanished on restart**.

Frontend half is on `feat/absorb-atrium` in pantheon-ui; end-to-end verification needs this image pinned on staging.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01Ups1TP9FXNqxbaaUXuEDrn

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `99489422a0b8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.