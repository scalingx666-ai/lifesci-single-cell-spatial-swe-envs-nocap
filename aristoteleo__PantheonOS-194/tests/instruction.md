# Issue

**Title:** feat(desktop): address a request to a screen, instead of asking the room

## Description

Directed requests — `desktop_read` / `desktop_call` / `desktop_screenshot` and
everything else through `_desktop_request` — now resolve the chat's anchor
(#192) and stamp the event with that viewport's id. Every other viewport hears
it and ignores it.

That retires the Web Locks election for these. The election worked, but
**anonymously**: a copy acted and nobody could say afterwards which one had,
which was the single hardest thing about debugging this layer.

Two limits fall away with it.

**The ping is gone.** It existed because a fresh chat's first request could beat
the UI's subscription to that chat's stream, and streams do not replay — so
every directed request paid a handshake round trip first. The stream is
pod-scoped now, and a lease is better evidence of a live screen than a probe
that races. `_desktop_ping` and `_publish` are deleted with their last callers.

**A chat context is no longer required.** `_desktop_request` used to refuse with
"no chat context — cannot reach the desktop", which is why `desktop_open` could
not be called from a standalone desktop page *at all*. It now resolves to the
pod's most recently active viewport.

The failure text is specific for the same reason: *"no desktop to ask — no
viewport is open on this pod"* sends someone to open one, where *"the desktop
did not answer"* sent them looking for a bug in a desktop that was simply not
open.

Verified on staging (`sha-97b3648`):

| | |
|---|---|
| `desktop_open` from a page with **no chat** | ok, `win-30` — previously a hard refusal |
| `desktop_anchor` vs the page's real `__pantheonViewportId` | identical |
| `desktop_read` on a Terminal window | correctly refuses: not a packaged app, so no bridge — anchoring did its job |
| `desktop_windows` with no desktop open at all | answered from the document |

71 desktop tests pass. Browser half is on pantheon-ui `feat/absorb-atrium`: it
acts when addressed, and falls back to the old election only when an event
carries no `viewport_id` (a pod that predates this).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cc5be82cccf5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.