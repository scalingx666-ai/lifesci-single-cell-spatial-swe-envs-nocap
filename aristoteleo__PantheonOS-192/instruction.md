# Issue

**Title:** feat(desktop): who is looking — leased viewport and chat-client identity

## Description

The registry the anchoring design needs (`docs/desktop/anchoring.md` §3 in
pantheon-ui), and what presence has been blocked on. Until now the Web Locks
election was **anonymous**: a copy could act and nobody could name it afterwards
— which is why "which viewport answered?" was unanswerable throughout the
session work.

**Two identities, because the page is the wrong granularity.** A *viewport* is
something rendering the desktop; a *chat client* is one chat UI — one per Agent
app window — carrying the chat it shows and the host viewport in its own page.
That host field is the anchoring link: take a chat's clients, pick the most
recently active, follow its host. Three Agent windows in one page then resolve
to the same viewport with nothing to disambiguate, and a chat open in two places
anchors wherever the person last was.

A per-page `{viewport_id, chats: […]}` model — which is what the first draft of
the design had — can express neither of those.

**Registration is a LEASE.** Unregistering on close cannot be more than
best-effort: `pagehide` does not fire for a crash, a dropped network or a
sleeping laptop, and each would leave an entry claiming to be a live screen,
which an agent then waits out into "the desktop did not answer". So clients
renew (~15 s) and entries expire (~45 s); the explicit leave only makes the
common case instant.

Two things done deliberately:

- **Expiry is applied when the registry is read**, not merely swept — a
  reaper's period would otherwise be a window in which a dead tab is
  addressable.
- **Activity is real input, not the heartbeat** — or a tab left open overnight
  outranks the window someone is typing in.

**Where it lives:** a file under `flock`, boot-stamped so a dead container's
registry is discarded rather than restored as a crowd of ghosts — the same
discipline as the session document, for the same reason (the toolset is a
ProcessJob per toolset). But **not in** the session document: a heartbeat is not
a change anyone needs to hear, and folding it in would bump `seq` and fan out to
every viewport every few seconds per open tab. Membership changes broadcast;
renewals do not.

Three UI-only tools: `desktop_presence` (renew + read back),
`desktop_presence_leave`, and `desktop_anchor` — the last exposed rather than
kept internal because "why that screen?" is otherwise unanswerable after the
fact.

**Not in scope:** nothing is addressed by `viewport_id` yet. Rewiring
`desktop_read` / `desktop_call` / `desktop_screenshot` onto the anchor, and
retiring the Web Locks election for directed requests, is the next change.

14 new tests, all against an explicit clock — a TTL you have to sleep through is
a test nobody runs. 71 desktop tests pass.

Verified on staging (`sha-ed47717`) with two desktops open:

| | |
|---|---|
| both register | 2 viewports, ttl 45s / heartbeat 15s |
| after a real click in B, `desktop_anchor(chat)` | B's own viewport id, reason `hosts the chat` |
| close B | viewports back to 1 |
| anchor after B is gone | moves to A — not a dead page |

Browser half is on pantheon-ui `feat/absorb-atrium`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e77c4e5a14f7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.