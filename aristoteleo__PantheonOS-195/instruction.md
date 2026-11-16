# Issue

**Title:** feat(desktop): an ephemeral channel for state whose only version is the newest

## Description

`desktop_broadcast` relays a value to the pod's other viewports and forgets it:
nothing sequenced, nothing written to the record, nothing replayed to a viewport
that joins later.

That is the point rather than a limitation. A camera mid-drag has no version
worth sequencing, and restoring someone else's zoom at boot is not a feature —
so putting it in the session document would be wrong in both directions. What
must survive a reload goes through `desktop_intent` instead.

This is the transport for the sync protocol's `stream` keys (pantheon-ui
`docs/desktop/shared-session.md` §7). Cursors will use it too: only the latest
value matters, and it should vanish with the person who produced it.

Verified on staging (`sha-d82398a`) as part of the protocol, two viewports on
one Viv window:

| | |
|---|---|
| a channel edit in A | reaches the session document tagged with A's viewport id |
| B's own copy of the app | adopts it — `contrastLimits [11, 4242]` |
| the camera | reaches B (`{zoom: -2.5, target: [900,900,0]}`) |
| the camera in the document | **absent** — never sequenced, never persisted |

The browser half is on pantheon-ui `feat/absorb-atrium`, and it carries the
three faults that were stopping any of this from working: the app host never
reported back state the shell handed it, a viewport receiving a shared change
threw on cloning a Vue proxy and showed an error instead of adopting, and a
window opened in a second tab booted on the app's defaults and published them
over the group's.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b0a5d4cd5b4d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.